1. Sử dụng Poetry:
    # Cài đặt Poetry: $ pip install poetry

    # Khởi tạo một dự án mới: $ poetry new myproject

    # Khởi tạo từ một dự án có sẵn: $ poetry init

    # Thêm package vào dự án
    $ cd myproject
    $ poetry add flask requests
    # Xóa package khỏi dự án: $ poetry remove <package_name>

    # Cài đặt các package: $ poetry install

    # Chạy ứng dụng python: $ poetry run python your_script.py
    # Có thể dùng với pytest hoặc black: poetry run pytest 

    # Activate/Enroll the virtual environment: $ poetry shell
    # Exit virtual environment: $ deactivate

2. Sử dụng pip-tools:
    # pip-check: Giúp bạn kiểm tra dependencies và phiên bản hiện tại của các package.
    # pip-review: Cho phép bạn tự động cập nhật tất cả hoặc một số package cụ thể.
    # pip-sync: để cài đặt các package theo đúng phiên bản
    # pip-tools: Bao gồm pip-compile và pip-sync, giúp bạn tạo ra một file requirements.txt tối ưu với phiên bản tương thích và sử dụng file này để cài đặt hoặc đồng bộ hóa các package.
    # pip-compile: để tạo file requirements.txt​ {pip-compile requirements.in (requirements.in không yêu cầu tên phiên bản)}
    
    # Cài đặt pip-tools: $ pip install pip-tools

    # Tạo file requirements.in và liệt kê các package mà bạn cần (không cần phiên bản cụ thể).
    $ echo "flask \nrequests" > requirements.in

    # Sử dụng pip-compile để tạo file requirements.txt
    $ pip-compile requirements.in

    # Sử dụng pip-sync để cài đặt các package theo đúng phiên bản
    $ pip-sync