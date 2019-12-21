## Function replace Parameter 
###### Example Result : "Hello ${test}" to "Hello Joy"

```
	public static String replacePattern(String str, ArrayList param) throws Exception{
		String result = str;
		int n = 0;
		try{
			if (str.indexOf("${")>-1) {
				Pattern pattern = Pattern.compile("\\$\\{([^\\}]*)\\}");
				Matcher matcher = pattern.matcher(str);
				while (matcher.find()) {
					String strKey = (matcher.group(1));
					if(param.get(n) instanceof Date){
						Format formatter = new SimpleDateFormat(strKey, Locale.US);
						result = result.replaceFirst("\\$\\{"+strKey+"\\}", formatter.format(new Date()));
					} else {
						result = result.replaceFirst("\\$\\{"+strKey+"\\}", param.get(n).toString());
					}
					n++;
				}
			} 
		} catch(Exception e){		
			throw e;
		}
		return result;
	}
  ```

## Function invoke method
 ```
	public static String invokeMethodByName(Object obj, String methodName) throws Exception{
		String result = null;
		System.out.println("methodName : " + methodName);
		System.out.println("getDeclareMethod : " + obj.getClass().getDeclaredMethod(methodName));
		
		Object resultObj = obj.getClass().getDeclaredMethod(methodName).invoke(obj);
		if(resultObj!=null){
			result = resultObj.toString();
		}
		
		return result;
	}
 ```
###### Example : Invoke method "test" from class ServerUtils
 ```
	public static void main(String[] args){
		try{
			String result = KulNaJaUtil.invokeMethodByName(ServerUtils.class, "test");
			System.out.println("result : " + result);
		} catch(Exception e){
			e.printStackTrace();
		}
	}
 ```
