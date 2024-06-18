# 作業四報告 Guiding DIP Early Stopping with DDPM-inspired Supervision

姓名：盧湧恩

系級：資訊系113

學號：F74109040

Github: https://github.com/yungen-lu/Generative-Models-for-Visual-Signals-Assignment

## Method

在 DIP 中，我們的目標是訓練一個模型能夠從一個 random noise 中生成出一張圖片，其中訓練過程可以簡化為以下：

<img src="/Users/yungen/Fundamentals_and_Applications_of_Generative_AI/HW4/images/無標題-2024-06-09-2108.png" alt="無標題-2024-06-09-2108" style="zoom:50%;" />

我們可以借用 DDPM 的概念，在訓練的過程中不要讓 model 第一次就預測目標圖片，而是分成多個階段。每個階段的 noise 程度不同。讓模型在一開始訓練時不是預測目標圖片而是預測稍微沒有雜訊的圖片。詳細步驟為以下

1. 將目標圖片加上不同程度的 noise。 level 1 為最輕微、 level n 為最重的 noise

   <img src="/Users/yungen/Fundamentals_and_Applications_of_Generative_AI/HW4/images/stage.png" alt="stage" style="zoom:72%;" />

2. 將訓練階段拆成 n 個階段，每個階段的都有不同的訓練目標圖片，並且每個階段的訓練次數不須一樣（後續 Step scheduler 會詳細說明）

   <img src="/Users/yungen/Fundamentals_and_Applications_of_Generative_AI/HW4/images/無標題-2024-06-09-2108拷貝.png" alt="無標題-2024-06-09-2108拷貝" style="zoom:50%;" />

3. 依序執行每個階段的訓練

## Step scheduler

在實驗的過程中，發現每個階段的訓練次數影響到輸出結果。階段愈前面的訓練次數應該減少，而階段後面的訓練次數應該增加。

### Custom linear

<img src="/Users/yungen/Fundamentals_and_Applications_of_Generative_AI/HW4/images/custom_step.png" alt="custom_step" style="zoom:72%;" />

在前面 100 個訓練中每十個 iteration 就換到下一個階段



### Sigmoid

<img src="/Users/yungen/Fundamentals_and_Applications_of_Generative_AI/HW4/images/sigmoid_step.png" alt="sigmoid_step" style="zoom:72%;" />

使用 sigmoid 函數，最一開始時慢慢增加階段，然後快速增加階段到一定程度後在變成慢慢增加階段



## 實驗結果

* baseline (DIP paper 的 code)  以及我實作的版本比較 PSNR 值，可以看出我的版本更快得達到 30 PSNR

<img src="/Users/yungen/Fundamentals_and_Applications_of_Generative_AI/HW4/images/icvsb.png" alt="icvsb" style="zoom:72%;" />

* custom scheduler vs sigmoid scheduler

<img src="/Users/yungen/Fundamentals_and_Applications_of_Generative_AI/HW4/images/vs.png" alt="vs" style="zoom:72%;" />
