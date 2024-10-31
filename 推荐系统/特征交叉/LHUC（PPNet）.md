LHUC 这种神经网络结构，可以用于精排。LHUC 的起源是语音识别，后来被应用到推荐系统，快手将其称为 PPNet，现在已经在业界广泛落地。

视频中遗漏一个细节：将LHUC用于推荐系统，门控神经网络（2 x sigmoid）的梯度不要传递到用户ID embedding特征，需要对其做 stop gradient。




![alt text](image.png)

![alt text](image-1.png)