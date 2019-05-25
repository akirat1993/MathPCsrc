[TOC]

### 画像変換

```python
import torchvision.transforms as transforms
'''
transforms.ToTensor()
	PIL画像→[C][H][W] = 0~1(float32)に変換する
	白黒画像の場合はC=1,RGB画像の場合はC=3となっている
'''
```



### 便利機能

```python
'''
学習済み重みの一部を再利用する
	動機:
    転移学習をする際に特徴抽出は既存のネットワークを用いて行い,全結合層は自作する場合がある.その際に特徴抽出は学習済み重みを用いたい時がありその場合の対処法
  処理の注意点:
    model.load_state_dicで重みをloadする際には読み込む重み(学習済み重み)とmodelの重みの名前とサイズが完全一致する必要があるが,自作した層の重みは学習済み重みに含まれていない.そのため,自作した層の重みをmodel_state_dict()で取得しupdateで書き換えてmodelに戻してやるという処理を行う
  参考資料:
    (英語)
    https://discuss.pytorch.org/t/how-to-load-part-of-pre-trained-model/1113
'''
model = nn.Module
#学習済み重みのロード
state = torch.load(PATH)
model_state = model.state_dict()
#モデルにないパラメータや名前が同じでもサイズが異なるパラメータは削除
state = {k:v for k, v in state.items() if k in model_state and v.size() == model_state[k].size()}
model_state.update(state)
model = model.load_state_dict(model_state)
```



### 全体の流れ

```python

#複数GPUを使用する場合にgpu0番が必ず使われるのを防ぐ
if device != torch.device('cpu'):
  torch.cuda.set_device(device)

#訓練/テスト 
net.train();torch.set_grad_enabled(True)
#evalにすることでdropoutとbatch normalizationが評価モードになる
# with torch.no_grad():とtorch.set_grad_enabled(False)は等価
net.eval();torch.set_grad_enabled(False)

gpus = (0,)
device = torch.device(f'cuda:{min(gpus)}' if len(gpus) > 0 else 'cpu')

model = EnsFC(inp_size, n_class)
# use GPUs if necessary
if len(self.gpus) <= 1:
    model = model.to(self.device)
else:
    model = nn.DataParallel(model, self.gpus).cuda()
optimizer = optim.Adam(model.parameters(), lr = lr)

for X,y in dataloader:
    acurates.append(y)
    X = X.to(device); y = y.to(device)
    out = model(X)
    loss = F.cross_entropy(out, y)
    if sta == 'train':
        optimizer.zero_grad()
        loss.backward()
        optimizer.step()

#DropoutレイヤとBNレイヤをevaluationモード
net.eval()

#test
#with torch.no_grad(): torch.set_grad_enabled(False)

#checkpointとしてモデルを保存
path = 'checkpoint.tar'
torch.save(
    'model_state_dict':net.module.cpu().state_dict(),
    'optimizer_state_dict':optimizer.state_dict(),
    'epoch_info_dict': default_to_regular(epoch_info),
)

#
torch.save(model.module.state_dict(), PATH)

#optimizerも保存できる
optimizer = optim.SGD(model.parameters(), lr=0.1)
torch.save(optimizer.state_dict(), 'optimizer.pth')

##pytorchの重みの保存について詳しく書いてある
#https://qiita.com/mocobt/items/dd2e60fa2909bfa93b06

##重みの保存
model = models.resnet50(pretrained=True)
# modelの保存
torch.save(model.state_dict(), 'weight.pth')
model2 = models.resnet50()
#paralell gpu時のモデルの保存
#torch.save(model.module.cpu(),file_path)
#new_model = torch.load(file_path)

# パラメータの読み込み
param = torch.load('weight.pth')
model2.load_state_dict(param)
```

### データセット

```python
#----------------------------------------------------------------
#numpy 配列からdataloaderの作成
#----------------------------------------------------------------
#Xs,ys['train','test'] = np.array()
def mk_dataloaders_from_np(Xs, ys, batch_size, num_workers = 1):
    dataloaders = list()
    for sta in ['train', 'test']:
        Xs[sta] = torch.from_numpy(Xs[sta].astype(np.float32))
        ys[sta] = torch.from_numpy(ys[sta].astype(np.float32))
        #numpy->dataset(tensor)
        dataset = torch.utils.data.TensorDataset(Xs[sta], ys[sta])
        drop_last = True if sta == 'train' else False
        shuffle = True if sta == 'train' else False
        dataloader = torch.utils.data.DataLoader(dataset,
            batch_size=batch_size,shuffle=shuffle,num_workers= num_workers,
            drop_last = drop_last
        )
        dataloaders.append(dataloader)
    return dataloaders
```

### 高速に推論

pytorchではtrain時，forward計算時に勾配計算用のパラメータを保存しておくことでbackward計算の高速化を行っているらしい．
これは，`model.eval()`で行っていてもパラメータが保存されているようなので，下記対策が必要になる.[参考資料](https://qiita.com/sennbei/items/598365cf3b68955e11c5)

```python
def test(args, model, device, test_loader):
    model.eval()
    with torch.no_grad():
        model(data) # forward実行
```



### 描写

#### Transformsで変換した画像を複数枚描写

```python
from PIL import Image
import numpy as np

import torchvision
import torchvision.transforms as transforms
import matplotlib.pyplot as plt

'''
複数のPIL imageを同時に描写
Args:
    imgs (list)
        PIL imageのリスト
    nrow (int)
        1行あたりに描写する枚数
    size_scale (float)
        出力画像サイズのスケール(imgの何倍か)
    pad_value (float)
        画像の境界線の色(0->黒, 1->白)
'''
def draw_imgs(imgs, nrow = 2, size_scale = 1, pad_value = 0):
    H,W = np.array(imgs[0]).shape[:2] 
    #行数を計算
    ncol = len(imgpaths) // nrow
    if len(imgpaths) % nrow != 0:
        ncol += 1
    # fig size(pixel)
    figH = size_scale*ncol*H
    figW = size_scale*nrow*W 
    
    #piexl ->インチ(1インチ=2.54)
    plt.figure(figsize=(figH, figW))
    plt.axis("off")
    plt.imshow(
        np.transpose(
           torchvision.utils.make_grid(imgs, nrow = nrow, pad_value = pad_value),
            (1,2,0)
        )
    )

'''
transformsで変換した複数の画像を同時に描写

Args:
    imgpaths (list)
        描写したい画像パスのリスト
    transform_list (list)
        torchvision.transformsのリスト(list()でもOK)
        (例) [transforms.RandomHorizontalFlip()]
    n_row (int)
        1行あたりに描写する画像数
    rez_scale (float)
        元画像に対しての解像度(1以下)
    size_scale (float)
        元画像に対する出力画像サイズの大きさ
    pad_value (float)
        画像の境界線の色(0->黒, 1->白)
'''
def draw_transform_imgs(imgpaths, transform_list, nrow=2, rez_scale = 0.5, 
                        size_scale=0.5, pad_value=0):
    img = Image.open(imgpaths[0])
    H,W,C = np.array(img).shape[:3]
    
    #画像サイズを変更
    H_, W_ = int(H*rez_scale), int(W*rez_scale)
    transform_list.extend([
        transforms.Resize((H_, W_)),
        transforms.ToTensor()
    ])
    transform = transforms.Compose(transform_list)

    #変換画像(tensor)を作成
    imgs = [
        transform(Image.open(imgpath)) for imgpath in imgpaths
    ]
    print(f"Original Images NxCxHxW={len(imgpaths)}x{C}x{H}x{W}")
    print(f"Transposed Images NxCxHxW={len(imgpaths)}x{C}x{H_}x{W_}")
    
    draw_imgs(imgs, nrow = nrow, size_scale = size_scale/rez_scale, pad_value = pad_value)
    
#------------------------------------------
#サンプル
#------------------------------------------
import glob, random
#画像パスをリストとして取得
imgpaths = glob.glob(imgsrc+'/*') #imgsrc 描写する画像があるディレクトリパス(末尾に/はつけない)
#画像パスをランダムにn個取得
n_imgpaths = random.sample(imgsrc,4)

transform_list = [
    transforms.RandomHorizontalFlip()
]
draw_transform_imgs(n_imgpaths, transform_list, nrow=2, rez_scale = 0.5, size_scale=0.5)
```

