# Sửa lỗi chính tả tự động trên Tiếng Việt



## Dùng mô hình đã được train sẵn

1. Clone repository này về máy.
1. Tải các file trong thư mục sau về : https://drive.google.com/drive/folders/1pFecTPiMqcg7sIeebkM8QSerRN1pfTlb?usp=sharing, đặt chung với thư mục cloned.
2. Chạy file HardMasked_predict.ipynb. 

* Thư mục chứa toàn bộ data: https://drive.google.com/drive/folders/1En5uILZJUJrwa-BcFdwEWSWz60xrDeGY?usp=sharing

## Chi tiết các files
`Sua loi chinh ta tu dong.pdf` và `Spelling Error Correction using XLM-RoBERTa.pdf` trình bày chi tiết thí nghiệm và kết quả.

`crawltext.ipynb` chứa code thu thập dữ liệu từ các trang báo điện tử

`CreateData.ipynb` chứa code dùng để tạo dữ liệu training.

`Training_detector.ipynb` chứa code để huấn luyện detector.

`HardMasked_predict.ipynb` dùng để predict, sau khi đã huấn luyện detector.

`Spelling Error Correction using XLM-RoBERTa.pdf` report phương pháp.

Link bài viết tutorial: https://huynhnhathao.github.io/myblogs/2021/01/20/vietnamese-spelling-error-correction.html

## Train tokenizer và mô hình từ đầu

`random_vocab` dùng trong createData: https://drive.google.com/file/d/1VjHED1hE6i4Is-pLafQxkDXxFPsE5WyE/view?usp=sharing

### Train spm tokenizer

Tải về file text: https://drive.google.com/file/d/1mCkOhA8gYo01sdCuDmGyhCWw1aiDtF7Q/view?usp=sharing, dùng notebook CreateData.ipynb để huấn luyện spm tokenzer.

### Train detector

Để huấn luyện lại detector, cần tạo dữ liệu các từ sai chính tả theo hướng dẫn như trong file CreateData.ipynb.

## Tóm tắt:

- Mô hình này dùng để làm gì? : mô hình cuối cùng có thể dùng để nhận dạng và thay thế từ sai chính tả trong một câu thành một từ mới, *mà model cho là phù hợp hơn*.
- Mô hình cuối cùng tốt cỡ nào? : mô hình này có nhận ra được một từ sai chính tả hay không là phụ thuộc vào dữ liệu training của nó có đủ tốt hay chưa. Dữ liệu training tạo trong repository này vẫn chưa đủ tốt để nhận ra hầu hết các lỗi sai, nên muốn độ chính xác tốt hơn thì tạo dữ liệu tốt hơn.
- Mô hình hoạt động như thế nào? : mô hình cuối cùng gồm có 2 mô hình con, một cái có nhiệm vụ nhận ra từ sai chính tả và một cái điền vào chỗ trống. Project này chỉ tạo dữ liệu training và train mô hình dự đoán từ sai chính tả, còn việc điền vào chỗ trống thì đưa cho XLM-R masked language model làm. Nên nói đúng hơn thì nó không sửa từ sai chính tả mà là replace từ sai chính tả bằng từ mới, hên xui từ mới đó sẽ là từ đúng chính tả.
- Sao không làm cho nó đúng chất là một mô hình sửa chính tả luôn?: left as an exercise to the reader!
