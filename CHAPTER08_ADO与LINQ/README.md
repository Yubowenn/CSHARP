## ʵ��һ���������ݿ�

```c#
INSERT INTO dbo.[Table] VALUES(123,'Gates','1234567');

INSERT INTO dbo.[Table] VALUES(222,'Mike','1234567');

UPDATE dbo.[Table] SET Telephone = '88888' WHERE Stuname = 'Mike';

SELECT * FROM dbo.[Table];

DELETE FROM dbo.[Table] WHERE Id=123;


DELETE FROM dbo.[USER] WHERE username = 'CHENG';

SELECT * FROM dbo.[USER];

//�ȵ�SQL���
```


## ʵ�����ʵ���û���¼
```c#
[in Form1.cs]
using System;
using System.Collections.Generic;
using System.ComponentModel;
using System.Data;
using System.Data.SqlClient;
using System.Drawing;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows.Forms;

namespace loginaccount
{
    public partial class Form1 : Form
    {
        public Form1()
        {
            InitializeComponent();
        }

        private void button1_Click(object sender, EventArgs e)
        {
            try
            {
                string UserName = textBox1.Text.Trim();
                string PassWord = textBox2.Text.Trim();
                if (UserName == "")
                {
                    MessageBox.Show("�û���Ϊ�գ��������û���", "��ʾ", MessageBoxButtons.OK, MessageBoxIcon.Information);
                }
                else if (PassWord == "")
                {
                    MessageBox.Show("����Ϊ�գ�����������", "��ʾ", MessageBoxButtons.OK, MessageBoxIcon.Information);

                }
                else
                {
                    string str = "SELECT count(*) from Users WHERE username='" + UserName + "' and password = '" + PassWord + "'";
                    string connectionStr = "Data Source=(local)\\SQLEXPRESS;Initial Catalog=MYDB;Integrated Security=True";
                    SqlConnection conn = new SqlConnection(connectionStr); //�������Ӷ���
                    SqlCommand cmd = new SqlCommand(str, conn);//�����������
                    conn.Open();  //���һ�����Ӷ���򿪣���ô������try���ر���
                    Console.WriteLine("�������ӳɹ���");

                    SqlDataReader sdr = cmd.ExecuteReader(); //�������ݶ�ȡ������
                    sdr.Read();
                    sdr.Close();
                    int n = (int)cmd.ExecuteScalar(); //���ص�һ�У�����n
                    if (n >= 1)
                    {
                        MessageBox.Show("SUCCESS!");
                    }
                    else {
                        MessageBox.Show("�û������������", "����", MessageBoxButtons.OK, MessageBoxIcon.Warning);//����������ʾ�����벻��
                    }
                    conn.Close();
                }
            }
            catch (Exception ex)
            {
                MessageBox.Show(ex.Message);//��ӡ�쳣
            }
        }
    }
}
```