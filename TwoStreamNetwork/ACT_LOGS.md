### Dữ liệu cần chuẩn bị:
    1. Gloss
    2. Text
    3. Video
    4. Gloss mapping ID table
    5. Dùng HRNet để extract pose features: 
        https://github.com/HRNet/HRNet-Bottom-Up-Pose-Estimation
        https://github.com/HRNet/HigherHRNet-Human-Pose-Estimation

### Notes:
    1. Keypoints: Only needed in TwoStream;
    2. Two-stream network: một luồng xử lý hình ảnh và một luồng xử lý dữ liệu về keypoints.


### Training thử với Single Stream trước: (vì không cần dùng keypoint & chênh lệch BLEU + ROUGE ko quá 5%)
#### TODOs:
    1. [x] Export gloss from text: https://colab.research.google.com/drive/11NdMrUN6pdOAWm84fH_EnjREDw37Bk52?authuser=1#scrollTo=Jk8GGVOuz4fq&uniqifier=1
        Format: {
                    "name": <video name without extension>,
                    "signer": <number>,
                    "gloss": <text>,
                    "text": <text>,
                    "num_frames": <number>,
                    "sign": tensor([[0.]])
                }
    2. [x] Build mapping gloss vs ID table: https://colab.research.google.com/drive/11NdMrUN6pdOAWm84fH_EnjREDw37Bk52?authuser=1#scrollTo=Jk8GGVOuz4fq&uniqifier=1
    3. [x] Configure yaml file.
    4. [x] Tách video -> ảnh.
    5. [x] Download needed pretrain model for training SLT: 
            Link: https://hkustconnect-my.sharepoint.com/personal/rzuo_connect_ust_hk/_layouts/15/onedrive.aspx?id=%2Fpersonal%2Frzuo%5Fconnect%5Fust%5Fhk%2FDocuments%2Fpretrained%5Fmodels&ga=1
    6. [ ] Training on Kaggle: https://www.kaggle.com/code/toandaoicv/singlestreamsignlanguagetranslation/edit/run/166821736
        6.1. [x] Prune mBART Embedding & Add Gloss Embeddings:https://colab.research.google.com/drive/11NdMrUN6pdOAWm84fH_EnjREDw37Bk52?authuser=1#scrollTo=MSQ7zkGsjksC&uniqifier=1

    7. Fix lỗi missing translation_loss của model 
    Thêm vào class Seq2SeqLMOutput(ModelOutput) ở trong file có địa chỉ tương ứng với: 
    1. C:\Users\ADMIN\AppData\Local\Programs\Python\Python38\Lib\site-packages\transformers\modeling_outputs.py
    2. /usr/local/lib/python3.10/dist-packages/transformers/modeling_outputs.py
    Phần thêm:
    total_loss: Optional[Tuple[torch.FloatTensor, ...]] = None
    translation_loss: Optional[torch.FloatTensor] = None
    transformer_inputs: Optional[Tuple[torch.FloatTensor, ...]] = None
     