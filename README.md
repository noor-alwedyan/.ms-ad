my first ml project


feature_cols = [ 'order_number', 'order_dow', 'order_hour_of_day', 'days_since_prior_order', 'total_orders', 'avg_basket_size', 'reorder_ratio', 'mean_days_between_orders', 'last_order_recency', 'product_reorder_rate', 'avg_add_to_cart_order', 'prior_count', 'log_total_orders' ]
 for col in feature_cols: df_final[col] = df_final[col].astype('float32') df_final['reordered'] = df_final['reordered'].astype('int8') df_model = df_final[feature_cols + ['reordered']].copy() df_model.info()
 # تبدأ خطوة الclassification modeling: from sklearn.model_selection import train_test_split X = df_model.drop(columns=['reordered']) y = df_model['reordered'] X_train, X_test, y_train, y_test = train_test_split( X, y, test_size=0.2, random_state=42, stratify=y ) # هذه الخطوة تستخدم معى فقط logical regression, KNN, SVM: from sklearn.preprocessing import StandardScaler scaler = StandardScaler() X_train_scaled = scaler.fit_transform(X_train) X_test_scaled = scaler.transform(X_test) 
 خلاصة هاي الخطوة :
تم اختيار مجموعة من الميزات التي تمثل سلوك المستخدم، خصائص المنتج، وتوقيت الطلب.
بعد ذلك تم تقليل استهلاك الذاكرة باستخدام downcasting، ثم تقسيم البيانات إلى تدريب واختبار مع الحفاظ على توزيع الفئات.
أخيرًا، تم تطبيق Standard Scaling على الميزات لاستخدامها مع نماذج التصنيف الحساسة للمقياس.