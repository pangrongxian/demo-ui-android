# 融云

![Mou icon](http://www.rongcloud.cn/images/logo_1.png)





#### 运行条件

**AndroidStudio 0.6+**

**Gradle 1.11+**

**RongIMSDK**

**Android Support V4**

**Google GSON 2.2.+**

**听云SDK(Android Studio自动支持，Eclipse请安装开发插件或屏蔽6_FriendList中引用)**
**插件地址<http://download.networkbench.com/newlens/android_agent/eclipse>**

*如需使用自行申请APP_Key测试，需要搭建自己的auth服务器*

*测试服务器搭建请参照<https://github.com/rongcloud/auth-service-nodejs>*

服务器方面需要配置conf.json中的appKey属性完成验证

*在DemoContext中init方法中填入申请的APP_Key测试，并在DemoApi中配置HOST指向到自己的auth服务上*

*如适用Eclipse开发请Import路径app/src/main，编码请选择为 UTF-8。

#### 注意事项：
6_FriendList这个Demo演示在会话列表页面，点击右上角的添加按钮，先进入一空白页，通过点击空白页中的唯一一个按钮，进入选择好友页面，包括以下：
（1）MainActivity页即是会话列表页，注意extends FragmentActivity，而不是从Activity继承。代码如下

		public class MainActivity extends FragmentActivity implements OnClickListener{
		
		    ActionBar mActionBar;
		    ImageButton imageButton;
		    
		
		    @Override
		    protected void onCreate(Bundle savedInstanceState) {
		        super.onCreate(savedInstanceState);
		  
		        getIntent().setData(Uri.parse("rong://io.rong.imkit.demo").buildUpon().appendPath("conversationlist").appendPath("private")
		                .appendQueryParameter("targetId","user1").build());
		        setContentView(R.layout.activity_main);
		        mActionBar = (ActionBar)findViewById(android.R.id.custom);
		        mActionBar.getTitleTextView().setText("会话列表");
		        mActionBar.setOnBackClick(new View.OnClickListener() {
		            @Override
		            public void onClick(View v) {
		                finish();
		            }
		        });
		
		        LayoutInflater inflater = LayoutInflater.from(this);
		        imageButton = (ImageButton)inflater.inflate(R.layout.rc_imagebutton_selector,mActionBar,false);
		        
		        mActionBar.addView(imageButton);
		        
		        imageButton.setOnClickListener(this);
		    }
		
		
		    @Override
		  	public void onClick(View v) {
		  		// TODO Auto-generated method stub
		    	int imageButtonId = imageButton.getId();
		    	if(v.getId() == imageButtonId)
		    	{
			  		Intent intent = new Intent(MainActivity.this, TextActivity.class);
			        startActivity(intent);
		      	}
		  		
		  	}
		}

（2）MainActivity文件对应的activity_main.xml文件如下：
		<?xml version="1.0" encoding="utf-8"?>
		
		<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
		    android:orientation="vertical" android:layout_width="match_parent"
		    android:layout_height="match_parent">
		
		    <io.rong.imkit.veiw.ActionBar
		        android:id="@android:id/custom"
		        style="@style/RcTheme.ActionBar">
		    </io.rong.imkit.veiw.ActionBar>
		
		    <fragment
		        android:layout_width="match_parent"
		        android:layout_height="match_parent"
		        android:name="io.rong.imkit.fragment.ConversationListFragment"/>
		
		</LinearLayout>
（3）增加rc_imagebutton_selector.xml布局文件
	<?xml version="1.0" encoding="utf-8"?>
	
	<ImageButton xmlns:android="http://schemas.android.com/apk/res/android"
	    android:layout_width="wrap_content"
	    android:layout_margin="5dp"
	    android:layout_height="wrap_content"
	    style="@style/RcTheme.ActionBar.ButtonAdd"/>
（4）修改rc_theme.xml文件，在其中添加：
    <style name="RcTheme.ActionBar.ButtonAdd" parent="@android:TextAppearance.Small.Inverse">
	    <item name="android:gravity">center</item>
	    <item name="android:layout_height">wrap_content</item>
	    <item name="android:layout_width">wrap_content</item>
	    <item name="android:background">@drawable/rc_add_people</item>
	    <item name="android:textColor">@drawable/rc_co_select_selector</item>
    </style>
（3）增加TextActivity.java文件
		修改对应的布局文件activity_text.xml
		页面中加一Button按钮，实现点击时打开选择好友页，处理如下：
		@Override
		public void onClick(View v) {
  		  Intent intent = new Intent(TextActivity.this, RongActivity.class);
          intent.putExtra(RCloudConst.EXTRA.CONTENT, FriendMultiChoiceFragment.class.getName());
          startActivity(intent);
		} 	
    	
#### 联系我们
商务合作
Email：<bd@rongcloud.cn>

新浪微博 [@融云RongCloud](http://weibo.com/rongcloud)

客服 QQ 2948214065

公众帐号
融云RongCloud RongCloud 公众账号二维码

![Smaller icon](http://www.rongcloud.cn/images/code1.png "RongCloud")
