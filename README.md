# STS_multi_filters_CNN_by_word2vec_and_BERT

このソースコードは,SemEval-2014のSemanticTextualSimilarityというタスクを想定して作成した物である。

モデルの入力は"GoogleNews-vectors-negative300.bin.gz"という学習済みのWord2Vecを利用して単語を分散表現にした物と、"multi_cased_L-12_H-768_A-12
" という学習済みのBERTを利用して単語を分散表現にしたものである。
訓練データは、STS.input.OnWN.txt、STS.input.MSRvid.txt、STS.input.SMTeuroparl.txt、STS.input.tweet-news.txtの4つである。

モデルの特徴は、フィルターサイズが3、5、7の3つのフィルターを並行して利用しているところで、これにより多様な側面から文章の特徴を得ている。 また、畳み込みを行う前にSelf Attentionを行うことで、入力単語に対して重み付けを施している。 文ベクトルの作り方は、畳み込みとプーリング処理の後にGlobalAveragePoolingを利用することで作成している。 また、残差接続を施すことで、情報が落ちてしまうことを防いでいる。 文章の類似度は、cos類似度を利用して求め、3つの類似度の平均をとることで、アンサンブル学習を実現している。

精度は、テストデータSTS.input.images.txtに対して0.79である。
