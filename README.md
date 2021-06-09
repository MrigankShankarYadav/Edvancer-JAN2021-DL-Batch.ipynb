# Spam filter for Quora questions

This is Edvancer's deeplearning project . The data is available here https://www.dropbox.com/sh/kpf9z73woodfssv/AAAw1_JIzpuVvwteJCma0xMla?dl=0 Train file have 3 columns q_id , question_text , target . we need to find out whether a question_text is spam or not. so we can drop q_id column and predict the target column based on question_text. I am using glove embeddings to fill the values of embedding matrix in the embedding layer of the model . we can download glove embeddings from here http://nlp.stanford.edu/data/glove.42B.300d.zip . getting values from glove embeddings . embeding_index={}

f=open('glove.42B.300d.txt',encoding='utf-8')

for line in f: values=line.split() word=values[0] coefs=np.asarray(values[1:],dtype='float32') embeding_index[word]=coefs f.close()

After this we tokenize the data and padd the data based on max length

max_len=31

tk=Tokenizer(char_level=False,split=' ')

tk.fit_on_texts(x_train)

seq_train=tk.texts_to_sequences(x_train) seq_test=tk.texts_to_sequences(x_test)

vocab_size=len(tk.word_index)

seq_train_matrix=sequence.pad_sequences(seq_train,maxlen=max_len) seq_test_matrix=sequence.pad_sequences(seq_test,maxlen=max_len)

After padding the data we can build the lstm model
