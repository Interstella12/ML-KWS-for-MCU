with your own data
训练
python train.py --model_architecture dnn --model_size_info 144 144 144 --dct_coefficient_count 10 --window_size_ms 40 --window_stride_ms 40 --learning_rate 0.0005,0.0001,0.00002 --how_many_training_steps 10000,10000,10000 --summaries_dir work/DNN/DNN1/retrain_logs --wanted_words 'help,rob,helpren,kill,others'  --train_dir ./Events/ --data_url= --data_dir ./Events

测试
python test.py --model_architecture dnn --model_size_info 144 144 144  --dct_coefficient_count 10 --window_size_ms 40 --window_stride_ms 40 --wanted_words 'help,rob,helpren,kill,others'  --train_dir ./Events/ --data_url= --data_dir ./Events --checkpoint=./Events/best/dnn_9519.ckpt-9600


python freeze.py --model_architecture dnn --model_size_info 144 144 144 --dct_coefficient_count 10 --window_size_ms 40 --window_stride_ms 40 --wanted_words 'help,rob,helpren,kill,others' --checkpoint=./Events/best/dnn_9519.ckpt-9600 --output_file dnn_chkws.pb
 

wav测试
python label_wav.py --wav=./Events1/test/help/help_44100_229_3.wav --graph dnn_chkws.pb --labels ./Events/dnn_labels.txt --how_many_labels 1
python label_wav.py --wav=./Events1/test/rob/rob_44100_232_3.wav --graph dnn_chkws.pb --labels ./Events/dnn_labels.txt --how_many_labels 1


量化权值
python quant_test.py --model_architecture dnn --model_size_info 144 144 144 --dct_coefficient_count 10 --window_size_ms 40 --window_stride_ms 40 --checkpoint=./Events/best/dnn_9519.ckpt-9600
量化模型



python quant_test.py --model_architecture dnn --model_size_info 144 144 144 --dct_coefficient_count 10 --window_size_ms 40 --window_stride_ms 40 --checkpoint=./Events/best/dnn_9519.ckpt-9600 --act_max 32 0 0 0 0
