##Function replace Parameter ${test}

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
