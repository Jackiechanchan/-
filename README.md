# -
软工作业
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace _1111
{
    class Program
    {
        static void Main(string[] args)
        {
            string message = ""; // 存储用户命令
            while (message != "exit")
            {
                Console.Write("wc.exe ");
                message = Console.ReadLine();               // 得到输入命令
                string[] arrMessSplit = message.Split(' '); // 分割命令
                int iMessLength = arrMessSplit.Length;
                string[] sParameter = new string[iMessLength - 1];
                // 获取命令参数数组
                for (int i = 0; i < iMessLength - 1; i++)
                {
                    sParameter[i] = arrMessSplit[i];
                }
                // 获取文件名
                string sFilename = arrMessSplit[iMessLength - 1];
            }

          
        }
       

    }
    public class WC
    {
        private string sFilename;    // 文件名
        private string[] sParameter; // 参数数组  
        private int iCharcount;      // 字符数
        private int iWordcount;      // 单词数
        private int iLinecount;      // 总行数
        
        
        // 初始化
        public WC()
        {
            this.iCharcount = 0;
            this.iWordcount = 0;
            this.iLinecount = 0;
            
        }
        // 参数控制信息
        public void Operator(string[] sParameter, string sFilename)
        {
            this.sParameter = sParameter;
            this.sFilename = sFilename;

            foreach (string s in sParameter)
            { 
              //  基本功能
              else if (s == "-c" || s == "-w" || s == "-l")
                {
                    break;
                }
                else
                {
                    Console.WriteLine("参数 {0} 不存在", s);
                    break;
                }
            } 
        }
        // 统计基本信息：字符数 单词数 行数
        private void BaseCount(string filename)
        {
            try
            {
                // 打开文件
                FileStream file = new FileStream(filename, FileMode.Open, FileAccess.Read, FileShare.Read);
                StreamReader sr = new StreamReader(file);
                int nChar;
                int charcount = 0;
                int wordcount = 0;
                int linecount = 0;
                //定义一个字符数组
                char[] symbol = { ' ', '\t', ',', '.', '?', '!', ':', ';', '\'', '\"', '\n', '{', '}', '(', ')', '+' ,'-',
              '*', '='};
                while ((nChar = sr.Read()) != -1)
                {
                    charcount++;     // 统计字符数

                    foreach (char c in symbol)
                    {
                        if (nChar == (int)c)
                        {
                            wordcount++; // 统计单词数
                        }
                    }
                    if (nChar == '\n')
                    {
                        linecount++; // 统计行数
                    }
                }
                iCharcount = charcount;
                iWordcount = wordcount + 1;
                iLinecount = linecount + 1;
                sr.Close();
            }
            catch (IOException ex)
            {
                Console.WriteLine(ex.Message);
                return;
            }


        }
        // 打印信息
        private void Display()
        {
            foreach (string s in sParameter)
            {
                if (s == "-c")
                {
                    Console.WriteLine("字 符 数：{0}", iCharcount);
                }
                else if (s == "-w")
                {
                    Console.WriteLine("单 词 数：{0}", iWordcount);
                }
                else if (s == "-l")
                {
                    Console.WriteLine("总 行 数：{0}", iLinecount);
                }
            }
            Console.WriteLine();
        }
        
    }
}
