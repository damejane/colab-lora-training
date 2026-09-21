# Colab LoRA Training Notebooks

Google Colab 上で動作する画像生成基盤モデル向け LoRA 完全自動学習ノートブック集です。
Google Drive 連携・複数ジョブ連続実行・自動キャプション前処理・セキュアなトークン管理に対応しています。

---

## 📓 ノートブック一覧

| モデル | ノートブック | Colabで開く | 説明 |
| :--- | :--- | :--- | :--- |
| **Qwen-Image 2.1** | `qwen_image21_lora_colab_v1.ipynb` | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/damejane/colab-lora-training/blob/main/qwen_image21_lora_colab_v1.ipynb) | Alibaba 最新基盤モデル (DiT 7B + Qwen3-VL 8B + RGBA VAE)。T2I & I2I 対応 |
| **Krea 2** | `krea2_lora_colab_v43.ipynb` | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/damejane/colab-lora-training/blob/main/krea2_lora_colab_v43.ipynb) | Krea-2-Raw ベースモデルの完全自動学習 (fal / ComfyUI 互換) |

---

## 🚀 使い方

### 1. 事前準備
1. **Hugging Face トークン**
   - [Hugging Face Settings > Tokens](https://huggingface.co/settings/tokens) から Read トークンを取得。
   - Colab の左サイドバーにある **🔑（シークレット）** に名前 `HF_TOKEN` として登録しておくと自動で読み込まれます（未登録時は実行時に入力プロンプトが出ます）。
2. **Google Drive にデータセットと設定を配置**
   - 学習させたいデータセット（画像 + `.txt` キャプション）を ZIP 圧縮して Google Drive にアップロードします。
   - `MyDrive/qwen_image21/jobs.json`（または `MyDrive/krea2/jobs.json`）を作成します。

#### `jobs.json` の設定例:
```json
{
  "jobs": [
    {
      "trigger": "my_character",
      "zip": "MyDrive/datasets/my_character.zip"
    }
  ],
  "resolution": 1024,
  "steps": 1200,
  "lr": 1e-4,
  "rank": 32
}
```

### 2. ノートブックの実行
1. 上記の **「Open in Colab」** ボタンをクリックしてノートブックを開きます。
2. ランタイムのタイプを **GPU（L4 または A100 推奨）** に設定します。
3. セクション 1（トークン設定・Driveマウント・設定確認）を実行します。
4. メニューの **「ランタイム」→「以降のセルを実行」** を押せば、環境構築からモデルダウンロード、全ジョブ学習、Drive への LoRA 保存まで自動で完了します。