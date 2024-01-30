### 目錄結構
```
Pytorch-YOLOv8n
    ├─ docker
        ├─ Dockerfile                              # 依照不同硬體架構可能會需要改版(需在Dockerfile檔名後方加入_<硬體>，如：Dockerfile_GPU)，可再於run.sh中設定所要建立的版本
    ├─ engine/...                                  # 引擎執行過程中所需搭配的自定義程式庫，通常用於在run.sh時一併掛入docker的環境呼叫。                  
    ├─ tmp                                         # 系統的暫存路徑，必須需符合以下規範：
        ├─ datasets/<username>/<dataset>/...       # 使用者(username)選定的資料集，需透過後端Xdriver APIs自動pull進來
        ├─ logs/<username>/<dataset>.log           # 使用者(username)在執行run.sh過程中所產出的logs內容
        ├─ putputs/<username>/<dataset>/ ...       # 使用者(username)在執行完run.sh後，最終產生的檔案皆存放與此路徑
    ├─ spec.json                                   # 後端系統所需讀取的系統配置檔，必須包含以下資訊：
                                                     - 型態(dtype [str])
                                                     - 任務類型(task [str])
                                                     - 引擎名稱(name [str] )            *需與repo名稱相同, 但要將'-'換成'/'
                                                     - 輸出精度與格式(outputs [list])    *引擎輸出的模型規格，僅作為提供使用者參考的資訊
    └─ run.sh                                      # 後端系統調用引擎生命週期的Entrypoint，包含：建立docker環境 -> 掛載資料 -> 執行處理過程(engine) -> 輸出檔案 -> 清除暫存檔
```
