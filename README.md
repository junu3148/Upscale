# Video Upscale (Real-ESRGAN, IART) 

![image](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fa8616105-5508-4c8d-93f9-9e47a410cd89%2F6abb5902-362c-4a89-b339-e20eee707546%2F%25ED%2599%2594%25EB%25A9%25B4_%25EC%25BA%25A1%25EC%25B2%2598_2024-05-07_115341.jpg?table=block&id=2b35bce1-d4d8-4209-b8a8-a573fafdb3f5&spaceId=a8616105-5508-4c8d-93f9-9e47a410cd89&width=2000&userId=f73d4ca6-c265-4f94-8d39-cd6c6399751c&cache=v2)


## 사용 기술

### Spring boot Server

Open JDK 17, Spring boot, Gradle, Spring data JPA, Postgresql, 

GitHub, Docker, FFmpeg

### Flask Server

FastAPI, Python 3.8, PyTorch 2.3, CUDA 11.4,  OpenCV 4.9, FFmpeg

GPU - RTX 3060

Anaconda 3

AI model - codeformer, Real-ESRGAN

<a href="https://github.com/sczhou/CodeFormer">
    <img src="https://github.com/junu3148/Upscale/assets/134668162/cebd5c19-46bf-499b-81a1-a8b156c88e45" alt="CodeFormer Image">
</a>


FastAPI, Python 3.9, PyTorch 1.13, CUDA 11.7,  OpenCV 4.9, FFmpeg

AI model -  IART

<a href="https://github.com/kai422/IART">
    <img src="https://github.com/junu3148/Upscale/assets/134668162/0c664e1e-8135-4750-b463-f50a90f8323f" alt="IART Image">
</a>


---

## 담당한 기능

### Spring boot 서버 구현

- Upscale
    - 원본 파일 저장
    - FFmpeg 사용 2초 시간대 썸네일 추출 이미지 저장
    - Flask API 통신으로 Upscale된 비디오 저장
    - 영상의 메타정보와 함께 스트리밍 URL 경로 반환
- 히스토리 조회
    - AI 옵션에 맞는 작업 내용 리스트 조회

### Flask 서버 구현

- Upscale 엔드포인트
    - input 파일 저장
    - Real - ESRGAN을 통한 업스케일링
    - output 파일 저장
    - 파일 반환
    - 반환 후 파일 삭제

pip install fastapi

pip install uvicorn

pip install aiofiles

conda install -c conda-forge ffmpeg

### AI model 세팅 (Real-ESRGAN)

git clone this repository
git clone https://github.com/sczhou/CodeFormer
cd CodeFormer

create new anaconda env
conda create -n codeformer python=3.8 -y
conda activate codeformer

install python dependencies
pip3 install -r requirements.txt
python basicsr/setup.py develop
conda install -c conda-forge dlib (only for face detection or cropping with dlib)
conda install -c conda-forge ffmpeg

### AI model 세팅 (IART)

git clone https://github.com/kai422/IART
cd IART
pip install torch==1.13.1+cu117 torchvision==0.14.1+cu117--extra-index-url https://download.pytorch.org/whl/cu117
pip install -r requirements.txt

가중치 : https://drive.google.com/drive/folders/
1MIUK37Izc4IcA_a3eSH-21EXOZO5G5qU
경로 : ./experiments./pretrained_models/

pip install basicsr
pip install timm

conda install -c conda-forge ffmpeg

---

### 1. Postman 통신

![Untitled](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fa8616105-5508-4c8d-93f9-9e47a410cd89%2Fc3168894-360c-40e2-a4ef-c2c8790e6801%2FUntitled.png?table=block&id=b87d6a24-5cdd-4462-9206-d6cfa9141ba5&spaceId=a8616105-5508-4c8d-93f9-9e47a410cd89&width=2000&userId=f73d4ca6-c265-4f94-8d39-cd6c6399751c&cache=v2)

스프링 서버 엔드포인트

![Untitled](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fa8616105-5508-4c8d-93f9-9e47a410cd89%2F3b0052f0-2bf8-4ac2-acd5-4324a724d71a%2FUntitled.png?table=block&id=f819cf8e-e73b-4095-82ec-3e47bc676679&spaceId=a8616105-5508-4c8d-93f9-9e47a410cd89&width=2000&userId=f73d4ca6-c265-4f94-8d39-cd6c6399751c&cache=v2)


Flask 서버 엔드포인트

![Untitled](https://www.notion.so/image/https%3A%2F%2Fprod-files-secure.s3.us-west-2.amazonaws.com%2Fa8616105-5508-4c8d-93f9-9e47a410cd89%2F43da8291-fcac-4e3d-a66d-a83bb59cdeb8%2FUntitled.png?table=block&id=a6278f64-42d6-4cd1-8946-87f796b165bb&spaceId=a8616105-5508-4c8d-93f9-9e47a410cd89&width=1550&userId=f73d4ca6-c265-4f94-8d39-cd6c6399751c&cache=v2)

### 2. input Video (Real-ESRGAN)

[![Before Video](https://via.placeholder.com/400x300.png?text=Click+To+Watch+Before+Video)](https://file.notion.so/f/f/a8616105-5508-4c8d-93f9-9e47a410cd89/7ce1ec88-63bb-4c2f-b1fe-3897a012eab0/795e43dc-15de-4613-a650-6a731b18e1cd_Before.mp4?id=8319973e-8092-4090-92ab-f23d3df536ca)

[![Before Video (전설의고향)](https://via.placeholder.com/400x300.png?text=Click+To+Watch+%EC%A0%84%EC%84%A4%EC%9D%98%EA%B3%A0%ED%96%A5+Before+Video)](https://file.notion.so/f/f/a8616105-5508-4c8d-93f9-9e47a410cd89/9f3f9bbc-81bb-4c35-a3c7-50f57aef24ee/%EC%A0%84%EC%84%A4%EC%9D%98%EA%B3%A0%ED%96%A5_input.mp4?id=fddec1d6-102d-4952-8147-8fdc62ac7311)

### 3. output Video (Real-ESRGAN)

[![After Video](https://via.placeholder.com/400x300.png?text=Click+To+Watch+After+Video)](https://file.notion.so/f/f/a8616105-5508-4c8d-93f9-9e47a410cd89/57487d52-344e-4882-9b6c-022bb5f01478/795e43dc-15de-4613-a650-6a731b18e1cd_After.mp4?id=522a2a10-243c-443b-b0fe-f88046e3c940)

[![After Video (전설의고향)](https://via.placeholder.com/400x300.png?text=Click+To+Watch+%EC%A0%84%EC%84%A4%EC%9D%98%EA%B3%A0%ED%96%A5+After+Video)](https://file.notion.so/f/f/a8616105-5508-4c8d-93f9-9e47a410cd89/1f0d19df-fbdd-4b2b-b619-6e3d8963d466/%EC%A0%84%EC%84%A4%EC%9D%98%EA%B3%A0%ED%96%A5_Real_-_ESRGAN.mp4?id=23f2199d-32bc-49c6-b738-5a4d7b990fa6)


Codeformer를 사용하여 얼굴을 중점으로 복원하는 모델을 사용했습니다. 이 모델은 애니메이션에 특화되어 있어, 애니메이션의 완성도는 높았습니다. 그러나 영상의 사람 얼굴은 프레임마다 GAN 모델로 재생성되어, 영상을 결합했을 때 일관성이 유지되지 않았습니다.

### 1. 모델 (IART)

[CVPR 2024 Highlight] Enhancing Video Super-Resolution via Implicit Resampling-based Alignment
PWC PWC

Updates:

April 26, 2024: We released a new model trained on Vimeo-90K with DB degradation.

January 18, 2024: Check our updated paper with more illustrations, speed comparisons and additional qualitative results!

This is an offical PyTorch implementation of

[CVPR 2024 Highlight] Enhancing Video Super-Resolution via Implicit Resampling-based Alignment. [Paper]
Kai Xu, Ziwei Yu, Xin Wang, Michael Bi Mi, Angela Yao
Computer Vision and Machine Learning group, NUS.



Results


### 2. input Video (IART)

[구미호 축소 원본.mp4](https://file.notion.so/f/f/a8616105-5508-4c8d-93f9-9e47a410cd89/6c9f106a-d2bb-4275-8673-5786b005743d/%EA%B5%AC%EB%AF%B8%ED%98%B8_%EC%B6%95%EC%86%8C_%EC%9B%90%EB%B3%B8.mp4?id=a4c27757-db8d-4349-891f-aa4b8a0b5923&table=block&spaceId=a8616105-5508-4c8d-93f9-9e47a410cd89&expirationTimestamp=1715594400000&signature=KCrqGRpObf0fp2dN1qscwFb9fUMCr9Y5fqTrNNNcSh0)

### 3. output Video (IART)

[구미호 축소 변환본.mp4](https://file.notion.so/f/f/a8616105-5508-4c8d-93f9-9e47a410cd89/4e5f5a07-12e3-4d95-ba07-a252de47aa0c/%EA%B5%AC%EB%AF%B8%ED%98%B8_-_IART.mp4?id=5bc025df-647d-4d82-8a67-032f2d0bfc99&table=block&spaceId=a8616105-5508-4c8d-93f9-9e47a410cd89&expirationTimestamp=1715594400000&signature=DOesY-f7kZ_pKbgWfAw2nDUJFuEKKjlzFUXUUlFfU4s)
