>����ԭ����ת����ע��������[ԭ�Ĳ鿴��ϲ����](http://blog.csdn.net/qq137722697) http://blog.csdn.net/qq137722697

#��android���������ܡ�һ�����������첽����������MyHttpUtils���°���¼�¼���汾�ţ�2.X��
##һ��ǰ��
�������÷���[��Android��������ƪ��MyHttpUtilsһ���ǳ����õ��첽����������](http://blog.csdn.net/qq137722697/article/details/52414372)���й���ϸ�Ľ��ܡ������Ƕ�2.x�����ϸʹ�ý��ܣ���Դ�����Ȥ�Ļ������Ʋ�[github](https://github.com/huangdali/myhttputils)�˽�������Ϣ�����ó�����1����Ŀ��Ӧ�ø���ԭ��������okhttp��retrofit�ģ�2�������Volley��xUtils������̫�࣬�ܶ��ò��ϣ��ģ�3��ѧϰʹ�õġ�����Դ��Ļ��Ӧ��֪��MyHttpUtils�ײ����ͨ��HtttpUrlConnectionʵ�ֵģ���Android�׶���ʵ�ֵģ�����Ҫ����κε������Ŀ⡣
##�������ܽ���
1��֧��get��post����

2��֧��http��https��Э�飻

3��֧���������ӡ���ȡ��ʱʱ�䣨��ѡ����

4��֧��json��ʽ��������������json��ʽ�ิ�ӣ����ܸ㶨����

5��֧�ִ���JavaBean���󣨽���֮���javabean���󣩣�

6��֧�ֻص������з�Ӧ����javabean�������������ڻص�������ֱ���õ����������javabean����

7��֧�ֻص������и���UI�����Խ��첽�����ˣ���

��------------------������1.X�汾�Ĺ��ܣ�������2.x�汾�����Ĺ���---------------��

***8��֧���ļ����أ�������ô����ؽ��Ȼص�ѽ��***

***9��֧�ֵ��ļ��ϴ���***

***10��֧�ֶ��ļ��ϴ���***
>MyHttpUtils�����˴󲿷ֵ����������ˣ����ҷǳ�������Ŷ

##����ʹ�÷���
ʹ��gradle���������
```
 compile 'com.huangdali:myhttputils:2.0.2'
```

��Ȼ������Ȩ�޿ɱ����˼�Ŷ
```
 <uses-permission android:name="android.permission.INTERNET" />
```

�ļ��ϴ�������Ҳ��Ҫ���Ȩ�ޣ���Ҫ������ܵľͲ�Ҫ���ˣ�
```
 <uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
 <uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />
```
##�ġ�get����
����get�������������Ĳ�����ֱ��ƴ�ӵ��ӿڵĺ�߼��ɡ�

����ͨ��һ����ѯip��ַ��Ϣ��demo������get��ʽ��ʹ�ã����������е�Ч��ͼ����

![����](http://img.blog.csdn.net/20160902153934466)
�ϴ��룺
```
/**
     * ��ȡIP��ַ�ļ����¼�
     *
     * @param view
     */
    public void onGetIP(View view) {
        String url = "http://ip.taobao.com/service/getIpInfo.php?ip=182.254.34.74";//����Ľӿ�
        new MyHttpUtils()
                .url(url)//�����url
                .setJavaBean(IPBean.class)//������Ҫ�����ɵ�javabean����
                .onExecute(new CommCallback<IPBean>() {//�첽,����Ϊ�������javabean����
                    @Override
                    public void onSucess(IPBean ipBean) {//�ɹ�֮��ص�                      
                        ToastUtils.showMsg(MainActivity.this,ipBean.toString());
                    }
                    @Override
                    public void onFailed(String msg) {//ʧ��ʱ��ص�
                        Log.e("MyHttpUtilsDemo",msg);                       
                    }
                });
    }
```
����������˵����

***1��url������***��������Ľӿڵ�ַ����������ΪString��(**����**)

***2��setJavaBean������***���ý���֮���JavaBean���󣬼ǵü�.class����**����**��

***3��onExecute������***���ÿ�ʼ����get���ӿڣ��������ڻص������У�����ΪCommCallback���ɼӷ��͡���**����**��

***4��setReadTimeout������***���ö�ȡ��ʱʱ�䣨������ʱĬ��30s��������Ϊ���ͣ���λ�����롣��**��ѡ**��

***5��setConnTimeout������***�������ӳ�ʱʱ�䣨������ʱĬ��5s��������Ϊ���ͣ���λ�����롣��**��ѡ**��

>**�ر�˵��**�������������������ĵģ���ý����ַ������루UTF-8����ƴ�ӡ�
        `String text="";
        text= URLEncoder.encode(text,"UTF-8");`\\\����һ���쳣Ŷ


##�塢post����

����ͨ��һ����ȡ�û���ע���͸�����Ϣ��������˵��post���÷����ȿ�Ч��ͼ����

![����дͼƬ����](http://img.blog.csdn.net/20160902154311596)

�ϴ��룺
```
  public void onGetRemark(View view) {
        String remarkUrl = "http://192.168.1.161��8080/Test/userInfoController/updateUser.action";
        HashMap<String, String> param = new HashMap<>();
        param.put("userid", "7cf6871beeed856df47eb189");
        param.put("uid", "8011bddb58588ab54");
        new MyHttpUtils()
                .url(remarkUrl)
                .addParam(param)
                .setJavaBean(RemarkBean.class)
                .onExecuteByPost(new CommCallback<RemarkBean>() {
                    @Override
                    public void onSucess(RemarkBean remarkBean) {//�ɹ�֮��ص�
                       ToastUtils.showMsg(MainActivity.this,ipBean.toString());                      
                    }
                    @Override
                    public void onFailed(String msg) {//ʧ��ʱ��ص�
                       Log.e("MyHttpUtilsDemo",msg);   
                    }
                });
    }
}
```

����������˵����

***1��url������***��������Ľӿڵ�ַ����������ΪString��(**����**)

***2��setJavaBean������***���ý���֮���JavaBean���󣬼ǵü�.class����**����**��

***3��addParam():***����post����Ĳ���,����Ϊhashmap���͡���**����**��

***4��onExecuteByPost������***���ÿ�ʼ����post���ӿڣ��������ڻص������У�����ΪCommCallback���ɼӷ��͡���**����**��

***5��setReadTimeout������***���ö�ȡ��ʱʱ�䣨�����ü�ΪĬ��30s��������Ϊ���ͣ���λ�����롣��**��ѡ**��

***6��setConnTimeout������***�������ӳ�ʱʱ�䣨�����ü�ΪĬ��5s��������Ϊ���ͣ���λ�����롣��**��ѡ**��


>ͨ����������������ǲ��Ǿ��������ܺܺ��ã�ֻ��Ҫ��url��javabean�Ϳ����ڻص���������õ���Ҫ�Ľ������ᷢ����Ĵ�������û�������̡߳�û����handle����ʽ���ʹ�ô���ṹ���������������Rxjava��Retrofit��OkHttp��Ϥ�����ѿ϶��������ַ�ʽ������ʶ�ɡ�
##������ο���ͨ��json����javabean����
˵��ô�࣬����ܻ��Լ�������javabean���󣬿����ڱ����֪��Ҫ�����ˣ���ڽ�������ο���ͨ��json����javabean����֪�����Թ�����

�����Ѿ�������ȡΪһƪ���ͣ���Ϊ�ü�ƪ���Ͷ�Ҫ�������������鿴[\[android���ƪ\]��ο���ͨ��json����javabean����(GsonFormatʹ�ý̳�)](http://blog.csdn.net/qq137722697/article/details/52852804)  http://blog.csdn.net/qq137722697/article/details/52852804

##�ߡ��ļ�����
���������Լ���ı��ط������ӿ���Ϊ��ʾ���ϴ���
```      
        String url = "http://192.168.0.107:8080/UpLoadDemo/fg.exe";
        new MyHttpUtils()
                .url(url)
                .setFileSavePath("/sdcard/downloadtest")//��Ҫ����ֻ����д�ļ������·�����������ļ���Ŷ
                .setReadTimeout(5 * 60 * 1000)//���������ļ���ʱ�Ƚϴ��������ö�ȡʱ��Ϊ5����
                .downloadFile(new CommCallback<String>() {
                    @Override
                    public void onSucess(String msg) {
                        ToastUtils.showMsg(MainActivity.this, msg);
                    }

                    @Override
                    public void onFailed(String s) {

                    }

                    /**
                     * ������д���Ȼص�����
                     * @param total
                     * @param current
                     */
                    @Override
                    public void onDownloading(long total, long current) {
                        tvProgress.setText("��ǰ���ȣ�" + new DecimalFormat("######0.00").format(((double) current / total) * 100) + "%");
                    }
                });
```

��Ч����

![����дͼƬ����](http://img.blog.csdn.net/20161018230528084)

##�ˡ��ļ��ϴ�

�ļ��ϴ�---֧�ֵ��ļ��Ͷ��ļ��ϴ����������ϴ�֮ǰ�ȸ���һ�����ڽ����ļ��ķ�����루javaд�ģ�

###8.1������˴���(�Ѿ����ļ����սӿڵ��Թ�)

����˴�����һ���ǳ��򵥵�servlet������commons-fileupload�����ļ����ա�[jar������������](http://download.csdn.net/detail/qq137722697/9657409)
```
public class UpLoadServlet extends HttpServlet {
	private static final long serialVersionUID = -8705046949443366079L;

	public void doGet(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
	}

	public void doPost(HttpServletRequest request, HttpServletResponse response)
			throws ServletException, IOException {
		System.out.println("�����ˡ���������������");
		response.setCharacterEncoding("UTF-8");
		PrintWriter pw = response.getWriter();
//		String userId = request.getParameter("userid");
		// �����ļ���Ŀ��������
		DiskFileItemFactory factory = new DiskFileItemFactory();
		// �����ļ��ϴ�·��
		File uploadDir = new File(this.getServletContext().getRealPath(
				"/upload/"));// �����ļ��ϴ���·��Ϊ��Ŀ��/upload/userid/
		if (!uploadDir.exists()) {// ������ļ��в����ھʹ���
			uploadDir.mkdirs();
		}
		// ��ȡϵͳĬ�ϵ���ʱ�ļ�����·������·��ΪTomcat��Ŀ¼�µ�temp�ļ���
		String temp = System.getProperty("java.io.tmpdir");
		// ���û�������СΪ 5M
		factory.setSizeThreshold(1024 * 1024 * 5);
		// ������ʱ�ļ���Ϊtemp
		factory.setRepository(new File(temp));
		// �ù���ʵ�����ϴ����,ServletFileUpload ���������ļ��ϴ�����
		ServletFileUpload servletFileUpload = new ServletFileUpload(factory);
		try {
			List<FileItem> list = servletFileUpload.parseRequest(request);
			for (FileItem fileItem : list) {
				File file = new File(uploadDir, fileItem.getName());
				if (!file.exists()) {// �ļ������ڲŴ���
					fileItem.write(file);// �����ļ�
				}
			}
			pw.write("{\"message\":\"�ϴ��ɹ�\"}");
			System.out.println("{\"message\":\"�ϴ��ɹ�\"}");
		} catch (Exception e) {
			pw.write("{\"message\":\"�ϴ�ʧ��\"}");
			System.out.println("{\"message\":\"�ϴ�ʧ��\"}");
		}
	}
}
```
###8.2�����ļ��ϴ�

�������ϴ�sd���е�һ��index.png���ļ���С342KB��ͼƬ��demo��ʾ���ļ��ϴ����ϴ���:
```
new MyHttpUtils()
                .url("http://192.168.0.107:8080/UpLoadDemo/upload")
                .setJavaBean(UploadResultBean.class)
                .addUploadFile(new File("/sdcard/index.png"))//�������ϴ��ļ�
                .uploadFile(new CommCallback<UploadResultBean>() {
                    @Override
                    public void onSucess(UploadResultBean uploadResultBean) {
                        ToastUtils.showMsg(MainActivity.this, uploadResultBean.getMessage());
                    }

                    @Override
                    public void onFailed(String msg) {
                        ToastUtils.showMsg(MainActivity.this, msg);
                    }
                });
```

��Ч����

![����дͼƬ����](http://img.blog.csdn.net/20161018232647737)

###8.3�����ļ��ϴ�
�ϴ�����demo.exe(8M)��mylog.png(247K)�ļ����ϴ��룺
```
ArrayList<File>fileList=new ArrayList<>();//�ļ��б�
        fileList.add(new File("/sdcard/demo.exe"));
        fileList.add(new File("/sdcard/mylog.png"));
        new MyHttpUtils()
                .url("http://192.168.0.107:8080/UpLoadDemo/upload")
                .setJavaBean(UploadResultBean.class)
                .addUploadFiles(fileList)//�������ϴ��Ķ���ļ�
                .uploadFileMult(new CommCallback<UploadResultBean>() {
                    @Override
                    public void onSucess(UploadResultBean uploadResultBean) {
                        ToastUtils.showMsg(MainActivity.this, uploadResultBean.getMessage());
                    }

                    @Override
                    public void onFailed(String msg) {
                        ToastUtils.showMsg(MainActivity.this, msg);
                    }
                });
```

��Ч����

![����дͼƬ����](http://img.blog.csdn.net/20161018234111648)


##�š����ص�ַ

Դ�뼰demo���ص�ַ��https://github.com/huangdali/MyHttpUtilsDemo����ӭstar��


>�����ҵĲ�����ҳ�˽����֪ʶ��http://blog.csdn.net/qq137722697


----------


>�����ҵ�github��ҳ�˽���࿪Դ��ܣ�https://github.com/huangdali
