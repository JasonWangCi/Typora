```java
    @RequestMapping(value = "/testCITokenAPI", method = RequestMethod.POST)
    @ResponseBody
    public Object testCITokenAPI(HttpServletRequest request, HttpServletResponse response) throws Exception {
        //step1 get prodToken
        String url = "https://idbroker.webex.com/idb/token/6078fba4-49d9-4291-9f7b-80116aab6974/v2/actions/GetBearerToken/invoke";
        List<String[]> headers = new ArrayList<>();
        headers.add(new String[]{"Content-Type","application/json"});
        String body = "{\n" +
                "  \"name\":\"moa_test_machina_account\",\n" +
                "  \"password\":\",1?0NOege,NY1Df_y9<j5@wRv10>8M>J\"\n" +
                "}";
        Map<String, String> map = HttpUtil.postWithBody(url,headers,body);
        String content = map.get("RESULT_CONTENT");
        JsonObject messageBodyObject = gson.fromJson(content, JsonObject.class);
        String currentString = messageBodyObject.get("BearerToken").getAsString();
        System.out.println("BearerToken:" + currentString);

        //step2 get accessToken
        String url2 = "https://idbroker.webex.com/idb/oauth2/v1/access_token";
        String token = "Basic Q2ZmODJiZGJhMzU4ZTMxM2M2YjJjMmY1ZmNkMmU4ODA1ZGNiODUwMjM0YmYwMDU4NzAyYjdlN2IxMmY3MzUzMzM6NDg4NzdhZmFjMjAwMDI4ZDA3ZjdiYWEyMTYxYTEwODkwMGNhNjdkZDJhMTY4NGExNzE3ZmRiNzJlZGJiZGE0Zg==";
        List<String[]> params = new ArrayList<String[]>();
        params.add(new String[]{"grant_type", "urn:ietf:params:oauth:grant-type:saml2-bearer"});
        params.add(new String[]{"scope", "Identity:OAuthKeyService Identity:Organization moa-api:moa-read qa-cmc:qa_cmc_api prod-cmc:prod_cmc_api china-cmc:china_cmc_api wbxoauth:user_authentication"});
        params.add(new String[]{"assertion", currentString});

        List<String[]> headers2 = new ArrayList<String[]>();
        headers2.add(new String[]{"Authorization", token});

        Map<String, String> result = HttpUtil.request(HttpUtil.POST, url2, headers2, params);

        String RESULT_CONTENT = result.get("RESULT_CONTENT");
        JsonObject messageBodyObject2 = gson.fromJson(RESULT_CONTENT, JsonObject.class);
        String token2 = messageBodyObject2.get("access_token").getAsString();
        System.out.println(result);
        System.out.println(token2);

        //step3 get oneTimeToken
        String url3 = "https://alpha.webex.com/authorization/identity/admintoken";
        List<String[]> params3 = new ArrayList<String[]>();
        params3.add(new String[]{"site", "alpha"});
        params3.add(new String[]{"username", "wbxadmin"});
        params3.add(new String[]{"userrole", "SITEADMIN"});
        params3.add(new String[]{"from", "LOGON"});
        params3.add(new String[]{"targeturl", "https://alpha.webex.com/alpha/default.php"});
        params3.add(new String[]{"actorid", "senwan"});
        params3.add(new String[]{"actorname", "senwan"});
        params3.add(new String[]{"actreason", "senwan"});

        List<String[]> headers3 = new ArrayList<String[]>();
        String token3 = "Bearer " + token2;
        headers3.add(new String[]{"Accept", "application/json"});
        headers3.add(new String[]{"Content-Type", "application/x-www-form-urlencoded"});
        headers3.add(new String[]{"TrackingID", "yyyyyyyyyTrackingIDTestByJasonyyyyyyyyyyy"});
        headers3.add(new String[]{"Authorization", token3});
        Map<String, String> result3 = HttpUtil.request(HttpUtil.POST, url3, headers3, params3);
        String content4 = result3.get("RESULT_CONTENT");
        JsonObject json4 = gson.fromJson(content4, JsonObject.class);
        System.out.println(json4);
        String token4 = json4.get("token").getAsString();
        System.out.println(result3);
        System.out.println(token4);


        //step4 go to site page
//        List<String[]> headers4 = new ArrayList<String[]>();
//        headers4.add(new String[]{"Content-Type", "application/x-www-form-urlencoded"});
//        headers4.add(new String[]{"TrackingID", "yyyyyyyyyTrackingIDTestByJasonyyyyyyyyyyy"});
//        List<String[]> params4 = new ArrayList<String[]>();
//        params4.add(new String[]{"token", token4});
//        String url4 = "https://alpha.webex.com/authorization/identity/adminlogin";
//        Map<String, String> result4 = HttpUtil.request(HttpUtil.POST, url4, headers4, params4);

        response.sendRedirect("https://train.qa.webex.com/authorization/identity/admintoken" + token4);
        return content;
    }
```



```java
    @RequestMapping(value = "/testAPPTokenAPI", method = RequestMethod.POST)
    @ResponseBody
    public Object testAPPTokenAPI(HttpServletRequest request, HttpServletResponse response) throws Exception {


        List<String[]> requestBody = new ArrayList<String[]>();
        List<String[]> header3 = new ArrayList<String[]>();

        String token = "SDJBUAAAAAEp3LZBpJnOfHwtDj/qIlHe0JoosI4rjN3h7ULnlNoAHwAAAYCyCw0I";
        String tokenWithAppname = "APP_WbxLogon".concat(":").concat(token);
        String appToken = "APPToken" + " " + Base64.getEncoder().encodeToString(tokenWithAppname.getBytes("UTF-8"));

        requestBody.add(new String[]{"site","train"});
        requestBody.add(new String[]{"username", "wbxadmin"});
        requestBody.add(new String[]{"userrole", "SITEADMIN"});
        requestBody.add(new String[]{"from", "LOGON"});
        requestBody.add(new String[]{"targeturl", "https://train.qa.webex.com/"});
        requestBody.add(new String[]{"actorid", "1"});
        requestBody.add(new String[]{"actorname", "userName"});
        requestBody.add(new String[]{"actreason", "trackingId"});

        header3.add(new String[]{"Accept", "application/json"});
        header3.add(new String[]{"Content-Type", "application/x-www-form-urlencoded"});
        header3.add(new String[]{"TrackingID", "trackingId"});
        header3.add(new String[]{"Authorization", appToken});
        String requestUrl = "https://train.qa.webex.com/authorization/identity/admintoken";
        Map<String, String> appTokenResult = HttpUtil.request(HttpUtil.POST, requestUrl, header3, requestBody);

        String content = appTokenResult.get("RESULT_CONTENT");
        JsonObject jsonObject = gson.fromJson(content, JsonObject.class);
        String accessToken = jsonObject.get("token").getAsString();

        String url = "redirect:https://train.qa.webex.com/authorization/identity/adminlogin?token=" + accessToken;
        return new ModelAndView(url);

//        redirect to target site pages
//        response.sendRedirect("https://train.qa.webex.com/authorization/identity/admintoken" + token4);
    }
```





```java
RESULT_CONTENT -> [{"ip":"10.244.36.1","dc":"DFW01","network":"10.244.36.0/22","vlan":"187","stack":"data","scope":"private","stack_alias":"WXP","service":"Meeting Centers","hostname":""}]
```



```java

```

