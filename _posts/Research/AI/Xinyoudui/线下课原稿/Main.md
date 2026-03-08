# Workflow

- 新建题目文件夹，将 baseline 复制到题目文件夹下
- 在题目文件夹新建 `data/` 文件夹，把数据放在 `data/` 文件夹下
- 通读 baseline，修掉 baseline 可能的隐藏 bug
- 调整全局文件路径
  - 训练数据
  - `.pth` 文件
- 根据环境变量，判断是否在线上评测系统（`ONLINE_JUDGE`）
  - 本地：训练、保存模型
    - 把模型保存在 `data/` 文件夹下
  - 线上：加载模型、测试
    - 可能需要更改 `device` 相关
      - 通过 `.to(device)` 确保测试时所有数据都在 GPU 上
      - `torch.load('xxx.pth', map_location=device)`
  - 可能需要自己写保存 / 加载模型的代码
- 训练，花费较长时间
- 将 `data/` 上传到[数据集](https://www.bohrium.com/dataset/list)，同时包含训练数据与模型参数
- ~~在本地创建假数据，进行测试~~
- 第一次提交
- 复制一份改完的 baseline 作为副本不要动
- 优化

提示：
- 对于二分类问题，若 baseline 分数约为 $0.5$，有可能是输出全都为 $0$ 或全都为 $1$。（2025 T4 宫格图）
- 提交 baseline 有分数，也不意味着 baseline 无 bug。（2025 T2 化学动力学问题）
- 提交 baseline 为 $0$ 分，也不意味着 baseline 有 bug。（2025 T1 组合词分割问题）

## 环境变量与路径修改

```py
ONLINE_JUDGE = True if os.environ.get('DATA_PATH') else False

if ONLINE_JUDGE:
    PATH = "/bohr/NOAI2024T3-qkf4/v1/data/"
else:
    PATH = "/personal/NOAI2024/T3/data/"

train_df = pd.read_csv(PATH + "train_news.csv")
```

# 炼丹

## 随机数设置

```py
def set_seed(seed=42):
    random.seed(seed)
    np.random.seed(seed)
    torch.manual_seed(seed)
    if torch.cuda.is_available():
        torch.cuda.manual_seed(seed)
        torch.cuda.manual_seed_all(seed)
```

## 预处理

- 归一化
- 标准化

## 数据增强

- 图片：旋转、翻转、裁剪、加入高斯噪声
- 文本：随机 mask、交换位置
- 设置概率 $p$，每个数据有 $p$ 的概率被增强。

## 模型优化

- 增加 layer 数
- `dropout`
- `BatchNorm` / `LayerNorm`
- `hidden_dim`
- 残差

## 优化训练过程

- Epoch 数
- Learning rate
  - 手动调
  - Weight decay
- Scheduler
  - Cosine annealing



# 环境配置

考试环境：https://www.bohrium.com/

## 在 `ipynb` 文件中使用 `torchvision`

使用镜像 `Basic Image:ioai:3.6` 即有可用环境。

## 在 `ipynb` 文件使用相对路径

```py
import os
os.chdir("/your/path/")
print(os.getcwd()) # test
```

## GPU 使用

- `batch_size` 拉大到 $128, 256$ 这个量级
- `DataLoader` 的线程数 `num_workers` 开大