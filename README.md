# Colab LoRA Training Notebooks

Google Colab 上で動作する画像生成基盤モデル向け LoRA 完全自動学習ノートブック集です。
Google Drive 連携・複数ジョブ連続実行・自動キャプション前処理・セキュアなトークン管理に対応しています。

---

## 📓 ノートブック一覧

| モデル | ノートブック | Colabで開く | 説明 |
| :--- | :--- | :--- | :--- |
| **Anima** | `anima_lora_colab_v1.ipynb` | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/damejane/colab-lora-training/blob/main/anima_lora_colab_v1.ipynb) | CircleStone Labs 2B DiT (Qwen3-0.6B + WanVAE)。LanPaint / ComfyUI 完全対応 (`sd-scripts` 版) |
| **Krea 2** | `krea2_lora_colab_v43.ipynb` | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/damejane/colab-lora-training/blob/main/krea2_lora_colab_v43.ipynb) | Krea-2-Raw ベースモデルの完全自動学習 (fal / ComfyUI 互換) |
| **Qwen-Image 2.1** | `qwen_image21_lora_colab_v1.ipynb` | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/damejane/colab-lora-training/blob/main/qwen_image21_lora_colab_v1.ipynb) | Alibaba 基盤モデル (DiT 7B + Qwen3-VL 8B + RGBA VAE)。T2I & I2I 対応 |

---

## 🚀 使い方 (簡単テンプレート・設定ファイル不要)

### 1. 事前準備
1. **Hugging Face トークン**
   - [Hugging Face Settings > Tokens](https://huggingface.co/settings/tokens) から Read トークンを取得。
   - Colab の左サイドバーにある **🔑（シークレット）** に名前 `HF_TOKEN` として登録しておくと自動で読み込まれます（未登録時は実行時に入力プロンプトが出ます）。
2. **Google Drive にデータセットを配置 (フォルダに入れるだけ！)**
   - `jobs.json` などの設定ファイルは**一切不要**です。
   - 学習させたいデータセット（画像 + `.txt` キャプション）の ZIP ファイルを、対応するモデルの `queue/` フォルダに配置します:
     - **Anima**: `MyDrive/anima/queue/`
     - **Krea 2**: `MyDrive/krea2/queue/`
   *(各モデルフォルダ直下に ZIP を置いた場合も、セル実行時に自動で `queue/` に移動されます)*

```
Google Drive フォルダ運用:
 📂 MyDrive/<model>/queue/    <-- 学習させたいZIPをここに入れる
 📦 MyDrive/<model>/done/     <-- 正常完了したZIPが自動移動
 💾 MyDrive/<model>/outputs/  <-- 完成したLoRAがここに自動納品
```

### 2. ノートブックの実行
1. 上記の **「Open in Colab」** ボタンをクリックしてノートブックを開きます。
2. ランタイムのタイプを **GPU（T4 / L4 / A100）** に設定します。
   - Anima は約 8〜10GB VRAM のため T4 でも快適に動作します。
   - Krea 2 は L4 または A100 推奨です。
3. セクション 1（トークン設定・Driveマウント・キュー確認）を実行します。
4. キュー一覧とトリガーワードを確認後、メニューの **「ランタイム」→「以降のセルを実行」** を押せば、環境構築からモデルダウンロード、全ジョブ学習、Drive への LoRA 保存まで自動で完了します。