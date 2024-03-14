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
    1. [x] Export gloss from text.
        Format: {
                    "name": <video name without extension>,
                    "signer": <number>,
                    "gloss": <text>,
                    "text": <text>,
                    "num_frames": <number>,
                    "sign": tensor([[0.]])
                }
    2. [x] Build mapping gloss vs ID table.
    3. [x] Configure yaml file.
    4. [x] Tách video -> ảnh.
    5. [ ] Download needed pretrain model for training SLT.
    6. [ ] Training.
