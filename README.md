my first ml project
قرأنا الملفات 1
2قللنا من حجم بيانات ال order_product
3 اعملنا دمج للبيانات بملف واحد df
4 اعملنا تشيك للداتا استخدمنا :head(),info(),describe()....
5 visulazition : لقيم ال nan value وعالجناها
6 اعملنا visulaization and distribution لل #days_since_prior_order ,order_hour_of_day ,add to cart order وفهمنا العلاقات للرسمات واستخدمناا ال kde لانه بيعمل الرسمة سموثر أكثر من ال histogram 
7 top_k_frequncey لل product_name  and aisles واعطاني شو المنتج والممرالاكثر طلبا ,
8 طلعت ال correlation لل using for numerical variable
9 وطلعت العلاقات لل corre;ation باستخدام مكتبة seabron and matblotlib and heatmab 
10 pairwise relationships
11 بينت بالرسم عدد الطلبات في اليوم وعدد الطلبات بالاسبوع 
12 عالجنا ال days_sice_prior_order بال sentinal باستخدام الصفر لانه ال missing اله معنى اذا كانت category يستخدم ال mode واذا كانت numerical بستخدم ال median ,واستخدمنا model_based باستخدام knn
13 عرضنا ال outlier برسمة ال matplotlib وعالجناها باستخدام ال IQR واستخدمنا clip 
14 اعملنا catigorical Encoding واستخدمنا ال dummy بس عمل تضخيم للذاكرة واستخدمت طريقة frequency encoding   بتفلل من مشكلة ال memory error
15 استخدمت one hot encoding for low cardinality and target/mean encoding for high cardinality 
16 Behavioral EDA
17 اعملنا ال feature engeeniring وقسمنا الداتا واعملنالم  دمج باستخدام merge واستخدمنا ال 
18 استخدمنا ال classification واستخدمنا النماذجknn,SVM,Logestic regression ,decison tree , randomForest and XGBoost
19 واعملنا regression واستخدمنا ال knn,SVM,Logestic regression ,decison tree , randomForest and XGBoost
حاولنا نطلع اوتبت ونقارن بس ضل يعطيني memory Error واستخدمنا اكثر من طريقة لنعالج المشكلة بس ما زبط 













































































feature_cols = [ 'order_number', 'order_dow', 'order_hour_of_day', 'days_since_prior_order', 'total_orders', 'avg_basket_size', 'reorder_ratio', 'mean_days_between_orders', 'last_order_recency', 'product_reorder_rate', 'avg_add_to_cart_order', 'prior_count', 'log_total_orders' ]
 for col in feature_cols: df_final[col] = df_final[col].astype('float32') df_final['reordered'] = df_final['reordered'].astype('int8') df_model = df_final[feature_cols + ['reordered']].copy() df_model.info()
 # تبدأ خطوة الclassification modeling: from sklearn.model_selection import train_test_split X = df_model.drop(columns=['reordered']) y = df_model['reordered'] X_train, X_test, y_train, y_test = train_test_split( X, y, test_size=0.2, random_state=42, stratify=y ) # هذه الخطوة تستخدم معى فقط logical regression, KNN, SVM: from sklearn.preprocessing import StandardScaler scaler = StandardScaler() X_train_scaled = scaler.fit_transform(X_train) X_test_scaled = scaler.transform(X_test) 
 خلاصة هاي الخطوة :
تم اختيار مجموعة من الميزات التي تمثل سلوك المستخدم، خصائص المنتج، وتوقيت الطلب.
بعد ذلك تم تقليل استهلاك الذاكرة باستخدام downcasting، ثم تقسيم البيانات إلى تدريب واختبار مع الحفاظ على توزيع الفئات.
أخيرًا، تم تطبيق Standard Scaling على الميزات لاستخدامها مع نماذج التصنيف الحساسة للمقياس.