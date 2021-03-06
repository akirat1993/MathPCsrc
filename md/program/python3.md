[TOC]

## コードの共通化

`gtx`などのサーバーの`~/.bash_profile`に以下を記載

```bash
if [ -d /mnt/data0/akirat/py3_util ]; then
	export PYTHONPATH='/mnt/data0/akirat/py3_util'
fi
```

## 頻出関数(自分用)

```python
 def return_adj_abspath(path):
    hostname = socket.gethostname()
    if hostname == 'ds-server':
        return path.replace('/mnt','',1)
    else:
        if path[:5] != '/mnt/':
            return '/mnt' + path
         else:
          	return path
```



## 便利関数

### np行/列ごとに違う関数を適用する方法の紹介

``` python
'''
numpy配列の行や列ごとに同じ関数を適用するのはnp.apply_along_axisという関数を用いて出来る.
(例えば行毎に小さい順に並び替えるとか)
それを応用して列ごとに違う関数を適用する方法の紹介
(今回は1列目は2倍, 2列目は3倍にしてみる)
'''
def double(x):
    return 2*x

def triple(x):
    return 3*x

def func(row):
    funcs = [double, triple]
    return [ funcs[i](v) for i,v in enumerate(row)]

# array([[0, 1],
#        [2, 3],
#        [4, 5]])
A = np.arange(6).reshape((3,2))

# array([[ 0,  3],
#        [ 4,  9],
#        [ 8, 15]])
A_ = np.apply_along_axis(func, 1, A)
```

## GPU

**GPUが使用可能な場合,特定の関数内で行列演算をGPUを用いて行うスクリプト**  
※MacなどGPUが使用不可の場合はCPUで計算を行います  

\#free memoryは基本的にはコメントアウトしていいです.
Cupyは一度mallocした領域を使い回すからです.

``` python
import numpy as np
try:
    import cupy as cp
    xp = cp
except:
    xp = np

def GPU_Sample(x):
    # convert to numpy to cupy if gpu is available
    x = cp.asarray(x) if xp != np else x
    x_n = x
    for i in range(10):
        x_n = xp.dot(x_n,x)
    #convert to cupy to numpy if necesssary
    x_n = cp.asnumpy(x_n) if xp != np else x_n
    #free memory
    #if xp != np:
    #    cp.cuda.set_allocator(cp.cuda.MemoryPool().malloc)
    return x_n

N = 5000
x = np.random.randn(N,N)
x_n = GPU_Sample(x)
```



## 画像Image

### 画像の読み込み+変換

``` python
from PIL import Image, ImageDraw, ImageFont
import numpy as np
import cv2
#小数点付きnp.arrayを0~255の数字に直す
imgArr = imgArr.astype(np.uint8)

#--------------------------------
# OpenCV (cv2imread)
#--------------------------------
#np [H][W][BGR] = 0~255
#RGBではないことに注意
BGRarr = cv2.imread(imgpath)

##CVの配列を=>PILに変換
RGBarr = BGRarr[:,:,::-1] #BGR->RGB
img = Image.fromarray(RGBrr)

#--------------------------------
# PIL Imageの処理
#--------------------------------
# PIL Imageの読み込み(jupyterで画像が表示される)
img = Image.open('/path/to/img')
#numpyに変換
#PIL => np[H][W][RGB] = 0~255
RGBarr = np.asarray(img)

#numpyから画像に変換
#RGBarr=[H][W][RGB] = 0~255 np.uinit8
img = Image.fromarray(RGBarr)

#PIL画像の保存
#qualityは1(最低)~95(最高)まで.デフォルトは75
img.save("tmp.png",quality=95)
```

### 画像処理

#### 切り取りCrop

``` python
# PIL ImageのCrop
#画像の左上は(xmin, ymin)
#xmin <= x < xmaxの範囲が切り取られる元画像は 0<=x<=W-1の範囲
#画像の領域外を選択すると黒に塗りつぶされる
#xminなどはfloat型でも良い
xmin = 0; ymin = 0; xmax = W; ymax = H  
crop_im = im.crop((xmin, ymin, xmax, ymax))
```

### PIL画像の描写

#### 単一画像の描写

```python
#figureは1つ
plt.figure() 
#plt.subplot(行数, 列数, 何番目のプロットか)
#何番目かは1始まりの英語の文章順
plt.subplot(1,1,1)
plt.imshow(PILimg)
#x,y座標の非表示
plt.axis('off')
```

#### 複数の図を描写1

``` python
# figure は 1 つ
plt.figure() # figureの縦横の大きさ

#(行数, 列数, 何番目)
#何番目かは1始まりの英語の文章順
plt.subplot(1,2,1)
plt.imshow(PILimg1)
plt.axis('off')

plt.subplot(1,2,2)
plt.imshow(PILimg2)
#x,y座標の非表示
plt.axis('off')

#複数の図の間隔を調整
plt.subplots_adjust(wspace=-0.3)
```

#### 複数の図を描写2

``` python
import torchvision.transforms as transforms
ToPILImage = transforms.ToPILImage()

'''
左に元画像をnum個,右に復元画像をnum個描写
    imgsT/reconsT:元画像/復元画像
        [N,C,H,W]
'''
def draw_OriRecon1(num, imgsT, reconsT, path = None):
    n = min(num, len(imgsT))
    #plt.figure()    
    _,_,h,w = imgsT.size()
    #(width, height)
    plt.figure(figsize=(w*2*n/100, h/100)) # figureの縦横の大きさ
    cnt = 1
    for tensors in [imgsT, reconsT]:
        for i in range(n):
            #(行数, 列数, 何番目)
            #何番目かは1始まりの英語の文章順
            plt.subplot(1,2*n,cnt)
            img = ToPILImage(tensors[i])
            plt.imshow(img)
            #x,y座標の非表示
            plt.axis('off')
            cnt += 1
            #plt.show()
    #図の余白を調整
    plt.subplots_adjust(left=0, right=1, bottom=0, top=1)
    #W = fig_width*dpi
    plt.savefig(path,dpi=100)
    
'''
左に元画像を右に復元画像をnum個描写
ori1, recon1
ori2, recon2
Args:
    imgsT/reconsT:元画像/復元画像
        [N,C,H,W]
'''
def draw_OriRecon2(num, imgsT, reconsT, path = None):
    n = min(num, len(imgsT))
    #plt.figure()    
    _,_,h,w = imgsT.size()
    #(width, height)
    plt.figure(figsize=(w*2/100, h*n/100)) # figureの縦横の大きさ
    cnt = 1
    for i in range(n):    
        for tensors in [imgsT, reconsT]:
            #(行数, 列数, 何番目)
            #何番目かは1始まりの英語の文章順
            plt.subplot(n,2,cnt)
            img = ToPILImage(tensors[i])
            plt.imshow(img)
            #x,y座標の非表示
            plt.axis('off')
            cnt += 1
            #plt.show()
    #余白を調整
    plt.subplots_adjust(left=0, right=1, bottom=0, top=1)
    #W = fig_width*dpi
    plt.savefig(path,dpi=100)
```



#### 白黒画像の描写

``` python
#白黒画像を表示
#Image.fromarray(arr[H][W]=0~255)において0->黒,125->gray, 255->白, 
Image.fromarray(arr.astype('uint8')*255)
```

#### ヒートマップを描写

``` python
#独自のヒートマップ作成
# Input:
#     arr(np): arr[h][w] = MinVal<=float<=MaxVal
#     MinHue,MaxHue:blue->220, red->360
# Output:
#     Blue2RedArr(np) [h][w][c] = RGB(0~255) 
def mk_blue_to_red_ImgArr(arr, MinVal = 0, MaxVal = 1, MinHue = 220, MaxHue = 360):
    H, W = arr.shape
    Blue2RedArr = np.ones((H,W,3))
    for h in range(H):
        for w in range(W):
            v = arr[h][w]
            if not MinVal <= v <= MaxVal:
                print('Error: Do not satisfy MinVal <= v <= MaxVal')
            else:
                #0~360
                hue = (MaxVal - v)/(MaxVal - MinVal)*MinHue - (MinVal - v)/(MaxVal - MinVal)*MaxHue
                hue/= 360
                Blue2RedArr[h][w][0] = hue
    #0~1
    Blue2RedArr = matplotlib.colors.hsv_to_rgb(Blue2RedArr)
    #0~255
    Blue2RedArr = np.uint8(Blue2RedArr*255)    
    return Blue2RedArr    
```

#### カラーバーを表示

``` python
#tick == False ->メモリを表示させない
def draw_colorbar(fpath, tick=True, c_map = "Blues"):
    a = np.array([[0,1]])
    pl.figure(figsize=(0.8, 9))
    img = pl.imshow(a, cmap= c_map)
    pl.gca().set_visible(False)
    cax = pl.axes([0.1, 0.2, 0.8, 0.6])
    pl.colorbar(orientation='vertical', cax=cax)
    if tick == False:
        plt.axis("off")
    pl.savefig(fpath)
    pl.close()
```

#### Backup

``` python
##Draw text and rectangels on PIL image------------
img = img.convert('RGBA')
# make a blank image for the text, initialized to transparent text color
txt = Image.new('RGBA', img.size, (255,255,255,0))
d = ImageDraw.Draw(txt)    
font = ImageFont.truetype(font_path, 25) #font_path = '/Library/Fonts/Arial Rounded Bold.ttf'
d.rectangle([left,top,right,bottom], outline='red')
d.multiline_text((w,h),'text',align='left',fill='red', font = font)
#--------------------------------------------------

#np.arrayで余白無しで保存
#np.array HxWxC
def save_1img(fpath,img):
    plt.figure(figsize=(img.shape[1]/100, img.shape[0]/100), dpi=100)
    #plt.savefig('myfig.png', dpi=1000)
    if len(img.shape) == 2:
        img = img.reshape(img.shape[0], img.shape[1])
        plt.imshow(img,'gray')
    elif img.shape[2] == 1:
        img = img.reshape(img.shape[0], img.shape[1])
        plt.imshow(img,'gray', vmin = 0, vmax = 1)
    else:
        plt.imshow(img,vmin = 0, vmax = 1)
    plt.axis("off")
    plt.subplots_adjust(left=0, bottom=0, right=1, top=1, wspace=0, hspace=0)
    #plt.savefig(fpath, bbox_inches = 'tight', pad_inches = 0.0,dpi=100)
    plt.savefig(fpath, dpi=100)
    plt.close()
```





## Parallel Processing

1. Sample

    ``` python
    from multiprocessing import Pool
    def hoge_f(x):
    	return x*2
    with Pool(processes=2) as pool:
    	 tl = [i for i in range(10)]
    	 result = pool.map(hoge_f, tl, 1)
    print(result)
    ```
