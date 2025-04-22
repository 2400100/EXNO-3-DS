## EXNO-3-DS

# AIM:
To read the given data and perform Feature Encoding and Transformation process and save the data to a file.

# ALGORITHM:
STEP 1:Read the given Data.
STEP 2:Clean the Data Set using Data Cleaning Process.
STEP 3:Apply Feature Encoding for the feature in the data set.
STEP 4:Apply Feature Transformation for the feature in the data set.
STEP 5:Save the data to the file.

# FEATURE ENCODING:
1. Ordinal Encoding
An ordinal encoding involves mapping each unique label to an integer value. This type of encoding is really only appropriate if there is a known relationship between the categories. This relationship does exist for some of the variables in our dataset, and ideally, this should be harnessed when preparing the data.
2. Label Encoding
Label encoding is a simple and straight forward approach. This converts each value in a categorical column into a numerical value. Each value in a categorical column is called Label.
3. Binary Encoding
Binary encoding converts a category into binary digits. Each binary digit creates one feature column. If there are n unique categories, then binary encoding results in the only log(base 2)ⁿ features.
4. One Hot Encoding
We use this categorical data encoding technique when the features are nominal(do not have any order). In one hot encoding, for each level of a categorical feature, we create a new variable. Each category is mapped with a binary variable containing either 0 or 1. Here, 0 represents the absence, and 1 represents the presence of that category.

# Methods Used for Data Transformation:
  # 1. FUNCTION TRANSFORMATION
• Log Transformation
• Reciprocal Transformation
• Square Root Transformation
• Square Transformation
  # 2. POWER TRANSFORMATION
• Boxcox method
• Yeojohnson method

# CODING AND OUTPUT:
       import pandas as pd
       df = pd.read_csv("Encoding_data.csv")
       df.head()
![372034180-3c4708b7-1e8e-404f-bfa4-ad9828da4d8b](https://github.com/user-attachments/assets/a1f8be27-69a9-4126-b4c0-0756958fc9d2)

        df.tail()

![373125493-69993b8c-66db-4689-8250-a37230bbcbae](https://github.com/user-attachments/assets/0b9c4b36-7f56-4212-ad7d-d4f611f1fa2b)

        df.describe()
![372034567-b470ef07-1cd5-4484-b711-9f61520d7e56](https://github.com/user-attachments/assets/d058fbc5-25b1-4e3f-9f8a-0060003e950a)

        df.info()
        
![372034715-b0a38927-ebd6-4b90-abd7-5b21436f8901](https://github.com/user-attachments/assets/ebe217c7-35e6-4dea-95ad-e4d50996016f)


       df.shape
       
![373125662-576d78f3-6747-422a-9a3f-31b79b218db7](https://github.com/user-attachments/assets/726be1e3-7471-48de-b6b6-137d40caaac1)


       df
![373126577-f62c2a51-ccd7-4888-bd01-1e29443f765f](https://github.com/user-attachments/assets/355859aa-3c4e-4a18-b180-72afe99a4ff2)



       #ordinal encoder
       from sklearn.preprocessing import LabelEncoder, OrdinalEncoder
       pm=['Hot', 'Warm','Cold']
       oe=OrdinalEncoder(categories=[pm])
       oe.fit_transform(df[["ord_2"]])
       
![373126198-af3fcacf-b7eb-457e-98d9-3889b41d7e2a](https://github.com/user-attachments/assets/e86558c4-a615-4a76-8607-17740cdeb983)

     df['bo2']=oe.fit_transform(df[["ord_2"]])
     df
![372035445-f4824aa3-72e2-4354-b39a-14d7bc6c5da8](https://github.com/user-attachments/assets/28b12b69-17df-4323-a516-162095529564)


      #label Encoder
      le=LabelEncoder()
      dfc=df.copy()
      dfc['ord_2']=le.fit_transform(dfc['ord_2'])
      dfc

![372035614-43d81ec8-49ab-43ef-888b-d7f097a39452](https://github.com/user-attachments/assets/24b7314a-5154-4aa8-9f3e-f826ffe8b20e)

        #One hot encoder
        from sklearn.preprocessing import OneHotEncoder
        ohe = OneHotEncoder(sparse = False)
        df2=df.copy()
        enc=pd.DataFrame(ohe.fit_transform(df2[["nom_0"]]))
        df2=pd.concat([df2,enc],axis=1)
        df2
![372035923-b1ddad21-90b8-4159-9548-8eca78a7dae5](https://github.com/user-attachments/assets/f3005878-8569-45a2-ac1d-1b3ff5b5a816)

      pd.get_dummies(df2,columns=["nom_0"])


![372036143-a0ea2434-a534-4afa-8b91-b17617c06e5a](https://github.com/user-attachments/assets/258eb641-f743-4f86-a7be-13c42d925aff)

      pip install --upgrade category_encoders
      from category_encoders import BinaryEncoder
      df= pd.read_csv("data.csv")
      df

![372036425-421dc1e1-fcb5-4202-87da-4517a20956d6](https://github.com/user-attachments/assets/05309a50-63b1-4d58-8787-6751fcde2568)

     #binary encoder
     be = BinaryEncoder()
     nd=be.fit_transform(df['Ord_2'])
     dfb=pd.concat([df,nd],axis=1)
     dfb1=df.copy()
     dfb
![372036654-9f44b784-9b99-41d2-8f29-39d3693cbbae](https://github.com/user-attachments/assets/8bc874cc-14d6-4204-afd8-f0b87a50783a)


     #target encoder
     from category_encoders import TargetEncoder
     te=TargetEncoder()
     cc=df.copy()
     new = te.fit_transform(X=cc["City"],y=cc["Target"])
     cc=pd.concat([cc,new],axis=1)
     cc

![372036827-f91f18ce-7e69-4cee-81a3-6bcf54b48958](https://github.com/user-attachments/assets/fcdd5506-2b40-4ec9-ba8a-8c04be857d3d)

       #Feature Transformation
       import pandas as pd
       from scipy import stats
       import numpy as np
       df=pd.read_csv("Data_to_Transform.csv")
       df

  
![372037136-3b1ec929-ad0e-47fb-b39a-03d9c228d6e1](https://github.com/user-attachments/assets/ace7df67-1065-4d44-9a5c-4db037038c6c)

      df.info()

![372037288-327ed0d1-2f8f-41c5-9da9-125c79d5d1ff](https://github.com/user-attachments/assets/4011944d-3bb7-4c23-b0cb-84d02608e902)


        df.describe()

![372037451-5f5c8f7a-49be-48dc-86c1-400a0214618d](https://github.com/user-attachments/assets/0b201aea-5f8e-4132-8af7-7bc30fd9876d)


        df.size

  ![372037588-4af8996e-d807-4ba2-8def-1ddcddca8d4d](https://github.com/user-attachments/assets/77bd6104-6b4e-47d6-97ee-d7b8187cf001)


       df.skew()
![372037729-8be208a6-db9f-4d23-abb3-7ccd8661225a](https://github.com/user-attachments/assets/81a1db95-8a29-44bb-bbb5-8198ee265b33)


      np.log(df["Highly Positive Skew"])

![372037918-78aafe8a-29e8-4602-94cf-04d5a6412c76](https://github.com/user-attachments/assets/1cd17fbe-3847-43ee-a817-b0cbc85c36fe)

    np.reciprocal(df["Moderate Positive Skew"])

![372038134-11e16ca2-36cc-4bb4-9ae2-8602167b6df5](https://github.com/user-attachments/assets/f9acd427-5bc2-4c17-935c-cb4e5db340ec)


     np.sqrt(df["Highly Positive Skew"])

 ![372038342-2b3b9469-a49c-4285-8c53-6158025da034](https://github.com/user-attachments/assets/56ca0d0d-fef0-4aa0-9fa6-f3ee00b20f78)


     np.square(df["Highly Positive Skew"])


![372038515-b2ee6d10-0ca8-4c43-8a5c-d1e425318246](https://github.com/user-attachments/assets/5009cb26-22a2-4473-abb7-e684dcd2d193)

    df["Highly Positive Skew_boxcox"], parameters=stats.boxcox(df["Highly Positive Skew"])
    df


![372038750-8715ef25-6571-4a90-b9a1-5d6ad36ccaf1](https://github.com/user-attachments/assets/1644ef49-1fad-43c6-ba4f-736e5d124e76)


     
    df["ModerateNegativeSkew_yeojohnson"],parameters=stats.yeojohnson(df["ModerateNegativeSkew"])
    df

    
![372039112-fda58aed-306d-4447-b66a-db7cdd0b233a](https://github.com/user-attachments/assets/17686049-d6ab-4323-9147-28dd6094eb0a)

    import matplotlib.pyplot as plt
    import seaborn as sns
    import statsmodels.api as sm
    import scipy.stats as stats
    sm.qqplot(df['Moderate Negative Skew'],line='45')
    plt.show()

![372039290-e4826368-b926-4d18-bc8f-7ff61372cc92](https://github.com/user-attachments/assets/f216ca3c-2227-4c3f-8b0a-95fe6ab6874a)


     from sklearn.preprocessing import QuantileTransformer
     qt=QuantileTransformer(output_distribution='normal',n_quantiles=891)
     
     df["Moderate Negative Skew"]=qt.fit_transform(df[["Moderate Negative Skew"]])


     sm.qqplot(df["Moderate Negative Skew"],line='45')
     plt.show()


  

![372039497-189e9be3-76c4-41ca-a7cf-63764cebec7b](https://github.com/user-attachments/assets/735150be-88c3-4475-b426-f78dd390edb0)

     df


![372039731-9a74678c-3e7c-4d20-96cf-c95e1b37707a](https://github.com/user-attachments/assets/5c818728-c5e9-46cd-b52f-24c54a0c7b84)


     df["Moderate Negative Skew_1"]=qt.fit_transform(df[["Moderate Negative Skew"]])
     sm.qqplot(df['Moderate Negative Skew'],line='45')
     plt.show()


     
![372039963-cdccbea2-1a33-4f3b-9ba3-95a12ac42751](https://github.com/user-attachments/assets/410a9870-36e7-4c0d-821a-d32f130cb207)


     df["Highly Negative Skew_1"]=qt.fit_transform(df[["Highly Negative Skew"]])
     sm.qqplot(df['Highly Negative Skew'],line='45')
     plt.show()
![372040112-c2a44890-9aee-4a59-808c-e5e43bd57817](https://github.com/user-attachments/assets/3fe75473-3c5d-4a3a-8c1a-9502bb740f03)

      
     sm.qqplot(df["Highly Negative Skew_1"],line='45')
     plt.show()
![372040288-b42704ee-86d4-4dee-8d41-544235bf59e3](https://github.com/user-attachments/assets/859c6501-8b98-4fde-9d70-9b436a394f91)


     sm.qqplot(np.reciprocal(df["Moderate Negative Skew"]),line='45')
     plt.show()

![372040456-13242ffc-05a2-467d-ba27-0c3555419b26](https://github.com/user-attachments/assets/d6f1b7ca-bf69-43a5-92df-677db51a19b1)

# RESULT:
  Thus the given data, Feature Encoding, Transformation process and save the data to a file was performed successfully.

       
