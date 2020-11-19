using Microsoft.VisualBasic.CompilerServices;
using System;
using System.Linq;
using System.Collections;
using System.Collections.Generic;


namespace PhanSo
{
    class PhanSo
    {
        private int tuSo;
        private int mauSo;

        public int TuSo { get => tuSo; set => tuSo = value; }
        public int MauSo
        {
            get { return mauSo; }
            set
            {
                try
                {
                    mauSo = value;
                    float a = TuSo / MauSo;
                }
                catch (DivideByZeroException)
                {
                    Console.WriteLine("Mau so sai");
                }

            }
        }

        public PhanSo()
        {
            TuSo = 0;
            MauSo = 1;
        }

        public PhanSo(int TuSo)
        {
            this.TuSo = TuSo;
            this.MauSo = 1;
        }

        public PhanSo(int TuSo, int MauSo)
        {
            
            if (MauSo == 0)
            {
                Exception exception = new Exception("Mau so phai khac 0");
                throw exception;
            }
            else if (MauSo > 0)
            {
                this.mauSo = MauSo;
                this.tuSo = TuSo;
            }
            else
            {
                this.mauSo = -MauSo;
                this.tuSo = -TuSo;
            }
            
        }

        private int UCLN(int a, int b)
        {
            if (a < 0)
            {
                a = -a;
            }

            int c = b;
            int r = a % c;
            while (r != 0)
            {
                a = c;
                c = r;
                r = a % c;
            }
            return c;
        }

        //private PhanSo PhanSoToiGian(PhanSo PS)
        //{
        //    int c = UCLN(PS.TuSo, PS.MauSo);
        //    PS.TuSo = PS.TuSo / c;
        //    PS.MauSo = PS.MauSo / c;
        //    return PS;
        //}

        public override string ToString()
        {
            int a = this.tuSo;
            int b = this.mauSo;
            int c = UCLN(a, b);
            this.tuSo /= c;
            this.mauSo /= c;
            return this.tuSo + "/" + this.mauSo;
        }

        public static PhanSo operator +(PhanSo PS1, PhanSo PS2)
        {
            int a = PS1.TuSo * PS2.MauSo + PS1.MauSo * PS2.TuSo;
            int b = PS1.MauSo * PS2.MauSo;
            return new PhanSo(a, b);
        }

        public static PhanSo operator -(PhanSo PS1, PhanSo PS2)
        {
            int a = PS1.TuSo * PS2.MauSo - PS1.MauSo * PS2.TuSo;
            int b = PS1.MauSo * PS2.MauSo;
            return new PhanSo(a, b);
        }

        public static PhanSo operator *(PhanSo PS1, PhanSo PS2)
        {
            int a = PS1.TuSo * PS2.TuSo;
            int b = PS1.MauSo * PS2.MauSo;
            return new PhanSo(a, b);
        }

        public static PhanSo operator /(PhanSo PS1, PhanSo PS2)
        {
            int a = PS1.TuSo * PS2.MauSo;
            int b = PS1.MauSo * PS2.TuSo;
            return new PhanSo(a, b);
        }

        public static bool operator >(PhanSo PS1, PhanSo PS2)
        {
            return PS1.TuSo * PS2.MauSo > PS2.TuSo * PS1.MauSo;
        }

        public static bool operator <(PhanSo PS1, PhanSo PS2)
        {
            return PS1.TuSo * PS2.MauSo < PS2.TuSo * PS1.MauSo;
        }

        public static void HonSo(PhanSo PS1)
        {
            int a = PS1.TuSo / PS1.MauSo;
            PhanSo PS2 = new PhanSo(a);
            PhanSo b = PS1 - PS2;
            Console.WriteLine("{0} chuyen ve dang hon so : {1}({2})", PS1, a, b);
        }

        

    }






    class Program
    {
        static void Main(string[] args)
        {
            PhanSo PS1 = new PhanSo(-1, 2);
            PhanSo PS2 = new PhanSo(1, -2);

            PhanSo Tong = PS1 + PS2;
            PhanSo Hieu = PS1 - PS2;
            PhanSo Tich = PS1 * PS2;
            PhanSo Thuong = PS1 / PS2;

            Console.WriteLine("2 phan so: {0}, {1}", PS1, PS2);
            Console.WriteLine("Cac phep tinh:");
             
            Console.WriteLine(" + : " + Tong);
            Console.WriteLine(" - : " + Hieu);
            Console.WriteLine(" * : " + Tich);
            Console.WriteLine(" / : " + Thuong);

            PhanSo PS3 = new PhanSo(2, 4);
            PhanSo.HonSo(PS3);

            Console.WriteLine(PS1 > PS2);

            var phansolist = new List<PhanSo>();
            phansolist.Add(new PhanSo(6, 3));
            phansolist.Add(new PhanSo(6, 5));
            phansolist.Add(new PhanSo(7, 3));
            phansolist.Add(new PhanSo(6, 7));

            Console.WriteLine("Hien thi list vua tao: ");
            foreach (PhanSo pi in phansolist)
            {
                Console.Write("{0} \t", pi);
            }

            PhanSo temp;
            for (int j = 0; j <= phansolist.Count - 2; j++)
            {
                for (int i = 0; i <= phansolist.Count - 2; i++)
                {
                    if (phansolist[i] > phansolist[i + 1])
                    {
                        temp = phansolist[i + 1];
                        phansolist[i + 1] = phansolist[i];
                        phansolist[i] = temp;
                    }
                }
            }

            Console.WriteLine("\nDay sap xep tang dan theo bubble sort:");
            foreach (PhanSo pi in phansolist)
            {
                Console.Write("{0} \t",pi);
            }


        }
    }
}
