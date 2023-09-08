# Sử dụng chatGPT

## Giới thiệu về chatgpt

### ChatGPT là gì?

  - ChatGPT (*Chat Generative Pre-training Transformer*) là một chatbot do công ty OpenAI phát triển. Có thể trả lời các câu hỏi về nhiều chủ đề như một trợ lý ảo.
  
  - Website: [chat.openai.com](chat.openai.com/)

### Truy cập ChatGPT bằng cách nào?

    - Lập tài khoản chatgpt
    - Dùng proxy: 10.6.33.11:8080

## ChatGPT có thể làm được gì?

1. Gợi ý nội dung cho 1 bài viết

    - *VD: Muốn viết một vấn đề mà chưa có ý tưởng về khung phân *

1. Dịch code sang ngôn ngữ khác

1. Định dạng dữ liệu

    - *VD: đưa 1 đoạn dữ liệu phi cấu trúc, chatgpt sẽ tự định dạng thành dạng bảng*

1. Makeup content

    - *VD: đưa ra các gạch đầu dòng trước, chatgpt tự điền nội dung*

1. Viết các loại codes

    - Tạo code từ đầu: *chỉ cần mô tả để chatgpt đưa ra 1 đoạn code*
    - Sửa lỗi code: *có thể copy lỗi vào đoạn chat để chatgpt đưa ra một đoạn code khác phù hợp hơn*
    - Viết chú thích trong code
    - Tổi ưu hóa code
    - Viết unittest 


## Cách sử dụng chatgpt hiệu quả

1. Đặt câu hỏi chi tiết, rõ ràng

1. Hỏi code theo các block nhỏ

1. Sử dụng các câu hỏi hay template sẵn được tổng hợp từ người dùng trước.

    - [Các mẫu câu hỏi được sắp xếp theo các chủ đề](https://www.awesomegptprompts.com/) 

    - [Các mẫu câu hỏi kèm hình ảnh câu trả lời theo các chủ đề](https://github.com/shoaibahmed/awesome-ChatGPT)

    - [ChatGPT Cheat Sheet for **Data Science**](https://www.datacamp.com/cheat-sheet/chatgpt-cheat-sheet-data-science)

    - [Các gợi ý khác](https://github.com/travistangvh/ChatGPT-Data-Science-Prompts)


## Tích hợp chatgpt vào các phần mềm thường dùng như vscode

- [ai-genie](https://github.com/ai-genie/chatgpt-vscode/)

- [ChatGPT Extension for VSCode](https://github.com/mpociot/chatgpt-vscode)

- [Other Extensions editors](https://github.com/Kamigami55/awesome-chatgpt#editors)

- [Chat bot](https://github.com/Kamigami55/awesome-chatgpt#chatbots)

- [Chia sẻ **pdf** kết quả đã chat với chatgpt](https://github.com/liady/ChatGPT-pdf)


## Những ứng dụng khác có thể thay thể chatGPT?

1. [**BingAI**](https://www.bing.com)

   - ChatGPT và Bing AI đều sử dụng các mô hình ngôn ngữ GPT (Generative Pre-trained Transformer), nhưng chúng là các nền tảng khác nhau. ChatGPT là một chatbot đa năng. Nó quét các tài nguyên như các *tạp chí học thuật, trang web kinh doanh, ấn phẩm và Wikipedia*.

    - Bing AI về cơ bản là một công cụ tìm kiếm được hỗ trợ bởi AI. Bing Chat chỉ cần đăng ký tài khoản trên bing và phải được cấp quyền truy cập đặc biệt mới có thể sử dụng nếu không thì sẽ tham gia danh sách chờ và đợi cấp quyền.

    - Bing Chat có khả năng chính xác hơn ChatGPT, bởi vì nó lấy từ nhiều thông tin gần đây hơn và dựa trên nhiều nguồn thông tin.

    - Nhược điểm của Bing Chat là không lưu lại lịch sử, cuộc chat sẽ bị xóa nếu bạn đóng tab mà bạn đang nói chuyện

1. **Bard**: Chưa được trải nghiệm

## Lưu ý

- Chatgpt giới hạn số từ trong câu hỏi nên không hỏi được câu quá dài

- Câu trả lời có thể không chính xác với câu hỏi realtime do dữ liệu huấn luyện có thể chưa được cập nhật (nhưng cũng đáp ứng khoảng 80%)

## Một số AI và library hay khác

- [https://askyourpdf.com/](https://askyourpdf.com/): Upload file pdf lên và hỏi các nội dung liên quan đến file này, có thể trả lời cả những câu hỏi không có trong file pdf
  
- [pandas-ai](https://github.com/gventuri/pandas-ai)
  
- [midjourney](https://www.midjourney.com): Tạo hình ảnh từ các mô tả

- [stable diffusion](https://stablediffusionweb.com/): Tạo hình ảnh từ các mô tả
- [runwayml](https://runwayml.com/): Tạo video ngắn từ các mô tả

## Lỗi thường gặp và cách xử lý

### Certificate vscode

1. Open link https://api.openai.com/v1/engines in Firefox and click on `cancel`
2. Download certificate for this in PEM (chain) and open in text editor
3. Check which ca file is used example for python
    ```python
    import certifi 
    print(certifi.where())
    ```
4. Copy the content of file in step 2 to the file in step 3 (at the bottom)
5. Run API code
