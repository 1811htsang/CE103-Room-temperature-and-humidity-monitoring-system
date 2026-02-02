# Giới thiệu
README này là phần hướng dẫn sử dụng đối với các artifact con thuộc về dự án.

# Cấu trúc thư mục artifactspace
Dưới đây là cấu trúc thư mục của artifactspace:
```
├── CMakeLists.txt      # Tập tin cấu hình CMake cho toàn bộ dự án
├── .gitignore          # Tập tin cấu hình Git để bỏ qua các tập tin/thư mục không cần thiết
├── .clangd             # Tập tin cấu hình cho trình phân tích mã nguồn Clangd
├── .devcontainer       # Thư mục cấu hình môi trường phát triển trong container
├── .vscode             # Thư mục cấu hình cho Visual Studio Code
├── lib                 # Thư mục chứa các thư viện tự phát triển
├── src                 # Thư mục chứa các triển khai của lib
├── sample              # Thư mục chứa các thư viện mẫu từ ESP-IDF API làm tiêu chuẩn thiết kế
├── test                # Thư mục chứa các tập tin kiểm thử theo unit test
├── main                # Thư mục chứa mã nguồn chính của dự án 
│   ├── CMakeLists.txt  # Tập tin cấu hình CMake cho mã nguồn chính
│   └── main.c          # Tập tin mã nguồn chính của dự án
└── README.md           # Đây là tập tin bạn đang đọc
```

This README is a sub-artifact served as an inner README or artifactspace of the main project (parent folder).

---

# Tiếng Anh

## Introduction
This README serves as a guide for the sub-artifact belonging to the project.

## Artifactspace Directory Structure
Below is the directory structure of the artifactspace:
```
├── CMakeLists.txt      # Folder configuration file for the entire project
├── .gitignore          # Git configuration file to ignore unnecessary files/folders
├── .clangd             # Configuration file for the Clangd source code analyzer
├── .devcontainer       # Configuration folder for the development environment in a container
├── .vscode             # Configuration folder for Visual Studio Code
├── lib                 # Folder containing self-developed libraries
├── src                 # Folder containing implementations of the libraries
├── sample              # Folder containing sample libraries from the ESP-IDF API as design standards
├── test                # Folder containing unit test files
├── main                # Folder containing the main source code of the project
│   ├── CMakeLists.txt  # Configuration file for the main source code
│   └── main.c          # Main source code file of the project
└── README.md           # This is the file you are currently reading
```