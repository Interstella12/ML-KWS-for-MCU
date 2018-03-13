训练
python train.py --model_architecture dnn --model_size_info 144 144 144 --dct_coefficient_count 10 --window_size_ms 40 --window_stride_ms 40 --learning_rate 0.0005,0.0001,0.00002 --how_many_training_steps 10000,10000,10000 --summaries_dir work/DNN/DNN1/retrain_logs --wanted_words 'help,rob,helpren,kill,others'  --train_dir ./Events/ --data_url= --data_dir ./Events

测试
python test.py --model_architecture dnn --model_size_info 144 144 144  --dct_coefficient_count 10 --window_size_ms 40 --window_stride_ms 40 --wanted_words 'help,rob,helpren,kill,others'  --train_dir ./Events/ --data_url= --data_dir ./Events --checkpoint=./Events/best/dnn_9519.ckpt-9600

持久化
python freeze.py --model_architecture dnn --model_size_info 144 144 144 --dct_coefficient_count 10 --window_size_ms 40 --window_stride_ms 40 --checkpoint work/DNN/DNN1/training/best/dnn_8425.ckpt-27600 --output_file dnn1.pb


文件标注
python label_wav.py --model_architecture dnn --model_size_info 144 144 144 --dct_coefficient_count 10 --window_size_ms 40 --window_stride_ms 40 --wav /tmp/speech_dataset/on/0a7c2a8d_nohash_0.wav --graph dnn1.pb --labels Pretrained_models/labels.txt --how_many_labels 3

量化权值
python quant_test.py --model_architecture dnn --model_size_info 144 144 144 --dct_coefficient_count 10 --window_size_ms 40 --window_stride_ms 40 --checkpoint work/DNN/DNN1/training/best/dnn_8425.ckpt-27600


量化模型
python quant_test.py --model_architecture dnn --model_size_info 144 144 144 --dct_coefficient_count 10 --window_size_ms 40 --window_stride_ms 40 --checkpoint=./Events/best/dnn_9519.ckpt-9600 --act_max 32 0 0 0 0
