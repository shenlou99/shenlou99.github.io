---
title: CSharp网络编程——TCP/IP编程
date: 2023-02-10 13:59:00
tags: C#,网络开发
categories: C#网络编程
---

## 一、Socket网络编程

Socket：套接字，用于描述IP地址和端口，是一个通信链的句柄，用以实现计算机之间通信。

有了服务器的IP地址和端口号，客户端才知道需要链接服务器哪个程序，建立socket连接。

## 二、TCP/UDP协议

- TCP协议：安全稳定，效率低，不会发生数据丢失。要求必须有一个服务器，因为要经历三次握手过程：
  - 1）客户端请求；
  - 2）服务器响应；
  - 3）客户端得知服务器响应
- UDP协议：效率高，但有可能发生数据丢失。不用经过服务器响应是否有空闲接收消息，自主传输。

## 三、创建客户端

1. 创建负责通信的socket

```C#
socketSend = new Socket(AddressFamily.InterNetwork,SocketType,Stream,ProtocolType.Tcp);
```

2. 获取将要连接的服务器的IP和程序的端口

```C#
IPAddress ip = IPAddress.Parse(txtServer.Text.Trim());
								   ↓
								 控件名
IPEndPoint point = new IPEndPoint(ip,Convert.ToInt32(txtPort.Text.Trim()));
														↓
								 					  控件名
```

3. 建立连接

```C#
socketSend.Connect(point);
ShowMsg("发送成功");
```

4. 给服务器发送消息

```C#
string str = txtmessage.Text.Trim();		//获取要发送的消息
  				 ↓
			   控件名
byte[] buffer = Encoding.UTF8.GetBytes(str);	//转成字节数组
socketSend.Send(buffer);					//发送字节数组
```

5. 不停的接收服务器发来的消息

```C#
注意：接收也要写在while(true)里面，需要一直接受客户端发过来的消息，并且需要创建后台新线程来执行它。
byte[] buffer = new byte[1024*1024*2];	//定义一个字节数组
int r = socketSend.Receive(buffer);		//接收字节数组放入buffer中，返回接收字节数
if(r == 0) return;				//如果没有信息接收，结束该循环
string str = Encoding.UTF8.GetString(buffer,0,r);		//将接收的字节数组转成字符串
ShowMsg(socketSend.RemoteEndPoint.Tostring() + ":" + str);
```

## 四、实例

#### 连接服务器：

```C#
 #region 连接服务器端
        private void btn_wangkouOPEN_Click(object sender, EventArgs e)
        {
            btn_wangkouOPEN.Enabled = false;
            //创建客户端Socket
            ClientSocket = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp);

            rtb_textshow.Text += "正在连接......" + "\n";
            //IP和端口号转换格式
            IPAddress ServerIP = IPAddress.Parse(tb_ipaddress.Text);
            int Port = int.Parse(tb_ipport.Text);
            //IP和端口号绑定
            IPEndPoint ServerAddress = new IPEndPoint(ServerIP, Port);

            try
            {
                //客户端Socket连接服务器地址
                ClientSocket.Connect(ServerAddress);
                SFlag = 1;  //若连接成功将标志设置为1
                rtb_textshow.Text += DateTime.Now.ToString("yy-MM-dd hh:mm:ss  ") + tb_ipaddress.Text + "连接成功" + "\n";
                btn_wangkouOPEN.Enabled = false;     //禁止操作连接按钮

                //开启一个线程接收数据
                th1 = new Thread(Receive);
                th1.IsBackground = true;
                th1.Start(ClientSocket);
            }
            catch
            {
                MessageBox.Show("服务器未打开");
                btn_wangkouOPEN.Enabled = true;
            }

            #region
            /*****
            serverIP = IPAddress.Parse(tb_ipaddress.Text);
            try
            {
                serverFullAddr = new IPEndPoint(serverIP, int.Parse(tb_ipport.Text));//设置IP，端口
                ClientSocket = new Socket(AddressFamily.InterNetwork, SocketType.Stream, ProtocolType.Tcp);
                //指定本地主机地址和端口号
                ClientSocket.Connect(serverFullAddr);
                //btnConn.Enabled = false;
                //rtb_textshow.Text = "连接服务器成功。。。。";
                MessageBox.Show("连接服务器成功！");
                btn_wangkouCLOSE.Enabled = true;
                //sock.Close();

            }
            catch (Exception ee)
            {
                btn_wangkouOPEN.Enabled = true;
                btn_wangkouCLOSE.Enabled = false;
                MessageBox.Show("连接服务器失败！");
                rtb_textshow.Text = "连接服务器失败。。。请仔细检查服务器是否开启" + ee;
                return;
            }
            ******/
            #endregion
        }
        #endregion
```

#### 断开网络连接

```C#
#region 断开网络连接
        private void btn_wangkouCLOSE_Click(object sender, EventArgs e)
        {
            //保证是在连接状态下退出
            if (SFlag == 1)
            {
                byte[] send = new byte[1024];
                send = Encoding.ASCII.GetBytes("*close*");  //关闭客户端时给服务器发送一个退出标志
                ClientSocket.Send(send);

                th1.Abort();    //关闭线程
                ClientSocket.Close();   //关闭套接字

                btn_wangkouOPEN.Enabled = true;  //允许操作按钮
                SFlag = 0;  //客户端退出后将连接成功标志程序设置为0
                rtb_textshow.Text += DateTime.Now.ToString("yy-MM-dd hh:mm:ss  ");
                rtb_textshow.Text += "客户端已关闭" + "\n";
                MessageBox.Show("已关闭连接");
            }

        }
        #endregion
```

#### 接收服务器端数据

```C#
 #region 接收服务器端数据
        void Receive(Object sk)
        {
            Socket socketRec = sk as Socket;

            while (true)
            {
                //5.接收数据
                //byte[] receive = new byte[4];                 //receive是十进制字节数组
                ClientSocket.Receive(receive);  //调用Receive()接收字节数据
                left_temp = receive[0];
                right_temp = receive[1];


                //6.打印接收数据
                if (receive.Length > 0)
                {
                    rtb_textshow.Text += DateTime.Now.ToString("yy-MM-dd hh:mm:ss  ") + "接收：";   //打印接收时间
                    //rtb_textshow.Text += byteToHexStr(receive) + "\r\n";  //将字节数据根据ASCII码转成字符串   //字符显示Encoding.ASCII.GetString(receive)        //16进制显示byteToHexStr(receive)
                    //rtb_textshow.Text += rtb_send.Text + "\r\n";                                                                                  //rtb_textshow.Text += BitConverter.ToInt32(receive,0) + "\r\n";
                    rtb_textshow.Text += "左边温度：" + left_temp + "\r\n";                       //已经是十进制了
                    rtb_textshow.Text += "右边温度：" + right_temp + "\r\n";    

                    //测试receive[0]数据类型
                    //rtb_textshow.Text += Convert.ToString(left_temp_high).GetType();                //system.string
                    //rtb_textshow.Text += receive[0];//.GetType();                                //receive[0] = 12 (ASCII码值）     //system.byte
                }
            }
        }
        #endregion
```

#### 向服务器端发送数据

```C#
 #region 向服务器端发送数据
        private void btn_send_Click(object sender, EventArgs e)
            {
                if (SFlag == 1)
                {
                    byte[] send = new byte[1024];
                    send = HexStringToByteArray(rtb_send.Text);
                    //send = Encoding.ASCII.GetBytes(rtb_send.Text);  //将文本内容转换成字节发送
                    ClientSocket.Send(send);    //调用Send()函数发送数据

                    rtb_textshow.Text += DateTime.Now.ToString("yy-MM-dd hh:mm:ss  ") + "发送：";   //打印发送数据的时间
                    rtb_textshow.Text += rtb_send.Text + "\n";   //打印发送的数据  rtb_send.Text + "\n"; 
                    rtb_send.Clear();   //清空发送框
                }
            }
        #endregion
```

