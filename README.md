# bert-Chinese-classification
bert中文分类实践

修改：
在run_classifier_word.py中添加NewsProcessor，即新闻的预处理读入部分 \
在main方法中添加news类型数据处理label \
 processors = { \
        "cola": ColaProcessor,\
        "mnli": MnliProcessor,\
        "mrpc": MrpcProcessor,\
        "news": NewsProcessor,\
    }
    
download_glue_data.py 提供glue_data下面其他的bert论文公测glue英文数据下载

data目录下是news数据的样例，按照样例构建自己的中文数据集，放在glue_data/NewsAll文件夹下

（由于大小限制，配置文件和数据集未上传）

首先自己下载中文配置文件chinese_L-12_H-768_A-12

包括bert_config.json/bert_model.ckpt/vocab.txt

解压后运行convert.sh(改成自己的绝对路径) 生成.bin文件

运行run.sh文件内容(改成自己的绝对路径)：

export GLUE_DIR=/search/odin/bert/extract_code/glue_data \
export BERT_BASE_DIR=/search/odin/bert/chinese_L-12_H-768_A-12/ \
export BERT_PYTORCH_DIR=/search/odin/bert/chinese_L-12_H-768_A-12/

python run_classifier_word.py \
  --task_name NEWS \
  --do_train \
  --do_eval \
  --data_dir $GLUE_DIR/NewsAll/ \
  --vocab_file $BERT_BASE_DIR/vocab.txt \
  --bert_config_file $BERT_BASE_DIR/bert_config.json \
  --init_checkpoint $BERT_PYTORCH_DIR/pytorch_model.bin \
  --max_seq_length 256 \
  --train_batch_size 32 \
  --learning_rate 2e-5 \
  --num_train_epochs 3.0 \
  --output_dir ./newsAll_output/ \
  --local_rank 3
  
  中文分类任务实践

eval_accuracy = 0.9281581998809113

eval_loss = 0.2222444740207354

global_step = 59826

loss = 0.14488934577978746
