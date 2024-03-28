### Dữ liệu cần chuẩn bị:
    1. Gloss
    2. Text
    3. Video
    4. Gloss mapping ID table
    5. Dùng HRNet để extract pose features: 
        https://github.com/HRNet/HRNet-Bottom-Up-Pose-Estimation
        https://github.com/HRNet/HigherHRNet-Human-Pose-Estimation
    6. Ảnh đầu vào cần resize về hình vuông: 512x512 (mặc định) hoặc theo trong configs.
### Notes:
    1. Keypoints: Only needed in TwoStream;
    2. Two-stream network: một luồng xử lý hình ảnh và một luồng xử lý dữ liệu về keypoints.
    3. Extract features sau khi train S2G.



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
     8. G2T -> đã train xong với BLEU4 score: 43.76 và ROUGE: 70.23
     9. Chưa train S2G -> extract features (S2G) -> train S2T: đến epoch 30 nhưng BLEU4 score: 1.78 và ROUGE: 5.83, WER: 96.4 -> STOP.
        2024-03-28 09:03:46,777 translation_loss Average:51.90
        2024-03-28 09:03:46,778 recognition_loss Average:72.28
        2024-03-28 09:03:46,779 total_loss Average:124.17
        2024-03-28 09:03:46,875 WER: 96.40
        2024-03-28 09:03:46,974 bleu1 5.83
        2024-03-28 09:03:46,975 bleu2 3.93
        2024-03-28 09:03:46,975 bleu3 2.53
        2024-03-28 09:03:46,975 bleu4 1.78
        2024-03-28 09:03:46,975 ROUGE: 5.83
        2024-03-28 09:03:46,977 best_score=1.79
     10. Train tiếp S2G -> extract features (S2G) -> S2T.