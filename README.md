# schema #
- ## [SchemaDeclaration](https://docs.totaljs.com/latest/en.html#api~SchemaDeclaration) #
    - ### 創建 SchemaInstance #
        - #### schema.create() #
            return SchemaInstance 
    - ### 定義欄位 #
        Schema要定義欄位，程式才有辦法幫你轉換資料
        - #### schema.define(name, type, [required], [custom]) ##
            - name：    欄位名稱
            - type：    欄位類型  
            - required： 是否為必要欄位
            - custom： 過濾條件
        - #### schema.define('prop name','Capitalize') ##  
            自動將欄位值轉換為PascalCase 命名規則
    - ### 列出所有欄位名稱 #
        - #### schema.fields ##
            Returns String Array  
            Returns all field names from the schema.
    - ### 清除所有欄位 #
        - #### schema.clear() ##
            return SchemaDeclaration
    - ### 註冊事件監聽函式 #
        - #### schema.addWorkflow(name,callback,[description]) #
            - name：事件名稱
            - callback：
                    
                    /** 
                    * 事件監聽函式
                    * error: 錯誤時呼叫
                    * model:事件傳送時攜帶資料
                    * controller:觸發事件的controller
                    * callback 成功執行完所呼叫函式 
                    */
                    function callback(error,model,controller,callback){}
            - description：optional 描述用
            - returns：回傳 SchemaDeclaration
        - #### schema.addHook(name,callback,[description]) #
            - name：事件名稱
            - callback：
                    
                    /** 
                    * 事件監聽函式
                    * error: 錯誤時呼叫
                    * model:事件傳送時攜帶資料
                    * controller:觸發事件的controller
                    * callback 成功執行完所呼叫函式 
                    */
                    function callback(error,model,controller,callback){}
            - description：optional 描述用
            - returns：回傳 SchemaDeclaration
    - ### 取得所有資料(回傳所有資料) #
        - #### schema.setQuery(callback,[description]) #
            - callback:

                    /** 
                    * 回呼函式
                    * error: 錯誤資料
                    * options: query(by get)或body(by post)
                    * callbback:觸發事件的controller
                    */
                    function(error,options,callback)
                    {
                        NOSQL('products').find().make(function(builder){
                            builder.callback(callback);
                        })
                    }
            - description：(optional) 描述用
            - returns：回傳 SchemaDeclaration
    - ### 取得單一筆資料(回傳符合條件的資料)  #
        - #### schema.setGet(callback,[description]) #
            - callback:

                    /** 
                    * 回呼函式
                    * error: 錯誤資料
                    * model: SchemaInstance(Schema實體)
                    * options : query(by get)或body(by post)
                    * callbback:觸發事件的controller
                    */
                    function(error,model,options,callback)
                    { 
                        NOSQL('products').one().where('name',options).callback(callback);

                    }
            - description：(optional) 描述用
            - returns：回傳 SchemaDeclaration
    - ### 儲存單一筆資料 #
        - #### schema.setSave(callback,[description]) #
            - callback:

                    /** 
                    * 回呼函式
                    * error: 錯誤資料
                    * model: SchemaInstance(Schema實體)
                    * options : query(by get)或body(by post)
                    * callbback:觸發事件的controller
                    */
                    function(error,model,options,callback){

                        NOSQL('products').update(model,true).where('id',model.id).callback(callback);

                    }
            - description：(optional) 描述用
            - returns：回傳 SchemaDeclaration
- SchemaInstance
- SchemaOptions
---