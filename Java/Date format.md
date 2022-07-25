Date format



Calendar calendar = Calendar.getInstance();

calendar.set(2018, 11, 31, 59, 59, 59);

Date happyNewYearDate = calendar.getTime();



​    String s = "09/22/2006";

​    SimpleDateFormat sd = new SimpleDateFormat("MM/dd/yyyy");

​    Date date1 = sd.parse(s);





Calendar c = Calendar.*getInstance*();

c.set(2022, 6, 22); 

Calendar c2 = Calendar.*getInstance*();

c2.set(2022, 6, 22); 

Date beginDate = c.getTime();

Date endDate = c2.getTime();



Calendar c = Calendar.*getInstance*();

c.set(2022, 6, 22); 

Date beginDate = c.getTime();



SimpleDateFormat b = new SimpleDateFormat("yyyy-MM-dd");

Date begin = new Date();

Date end = new Date();

String beginDate = b.format(begin);

String endDate = b.format(end);