# DGRPG-Game


using System;
using System.Data;
using System.Reflection.PortableExecutable;
using System.Security.Cryptography.X509Certificates;
using static DGRPGGame.Program;

namespace DGRPGGame
{
    internal class Program
    {
        private static Character player;



        static void Main(string[] args)
        {
            GameDataSetting();
            DisplayGameIntro();
        }

        static void GameDataSetting()
        {
            // 캐릭저 정보 세팅
            player = new Character("Chad", "전사", 1, 10, 5, 100, 1500);

            // 아이템 정보 세팅


        }

        static void DisplayGameIntro()  
        // 게임 인트로 부분이고, CheckValidInput을 통해 1.상태보기, 2.인벤토리를 입력시 들어갈수 있도록 만들었다.
        {
            Console.Clear();

            Console.WriteLine("스파르타 마을에 오신 여러분 환영합니다.");
            Console.WriteLine("이곳에서 던전으로 들어가기 전 활동을 할 수 있습니다");
            Console.WriteLine();
            Console.WriteLine("1. 상태보기");
            Console.WriteLine("2. 인벤토리");
            Console.WriteLine();
            Console.WriteLine("원하시는 행동을 입력해주세요.");

            int input = CheckValidInput(1, 2);
            switch (input)
            {
                case 1:
                    DisplayMyInfo();
                    break;
                case 2:
                    DisplayInventory();
                    break;
            }

        }

        static void DisplayMyInfo() // 상태보기를 누르면 나오는 MyInfo 화면입니다.
        {
            Console.Clear();

            Console.WriteLine("상태보기");
            Console.WriteLine("캐릭터의 정보를 표시합니다.");
            Console.WriteLine();
            Console.WriteLine($"Lv. {player.Level}");
            Console.WriteLine($"{player.Name}({player.Job})");
            Console.WriteLine($"공격력 : {player.Atk}");
            Console.WriteLine($"방어력 : {player.Def}");
            Console.WriteLine($"체력 : {player.Hp}");
            Console.WriteLine($"Gold : {player.Gold} G");
            Console.WriteLine();
            Console.WriteLine("0. 나가기");
            Console.WriteLine();
            Console.WriteLine("원하시는 행동을 입력해주세요.");


            int input = CheckValidInput(0, 0);
            switch (input)
            {
                case 0:
                    DisplayGameIntro();
                    break;
            }
        }

        static void DisplayInventory() // 인벤토리 창을 보여주는 화면입니다.
        {
            Console.Clear();

            Console.WriteLine("보유 중인 아이템을 관리할 수 있습니다.");
            Console.WriteLine();
            Console.WriteLine("[아이템 목록]");
            Console.WriteLine("- [E]무쇠갑옷 | 방어력 +5 | 무쇠로 만들어져 튼튼한 갑옷입니다.");
            Console.WriteLine("- 낡은 검 | 공격력 + 2 | 쉽게 볼 수 있는 낡은 검 입니다.");
            Console.WriteLine();
            Console.WriteLine("1. 장착 관리");
            Console.WriteLine("0. 나가기");
            Console.WriteLine();
            Console.WriteLine("원하시는 행동을 입력해주세요.");

            int input = CheckValidInput(0, 1);
            switch (input)
            {
                case 0:
                    DisplayGameIntro();
                    break;
                case 1:
                    DisplayEquipment();
                    break;
            }

        }

        static void DisplayEquipment() // 장착관리를 해보기 위해 작성했는데 잘 모르겠습니다.
        {
            Console.Clear();

            Console.WriteLine("[장비 목록]");
            Console.WriteLine("무쇠갑옷");
            Console.WriteLine("낡은 검");
            Console.WriteLine();

            Console.WriteLine("1번 입력시 장비 장착");
            Console.WriteLine("2번 입력시 장비 해체");
            Console.WriteLine();

            Console.WriteLine("0. 나가기");
            Console.WriteLine();
            Console.WriteLine("원하시는 행동을 입력해주세요.");

            int input = CheckValidInput(0, 0);
            switch (input)
            {
                case 0:
                    DisplayGameIntro();
                    break;
            }
        }


        static int CheckValidInput(int min, int max) 
        // CheckValidInput 으로 가장작은값~가장큰값 사이의 정수일경우 참(True)으로 if의 리턴 값을 출력하고, 그외에 거짓(False)일
        경우에는 "잘못된 입력입니다." 가 출력되도록 했습니다.
        {
            while (true)
            {
                string input = Console.ReadLine();

                bool parseSuccess = int.TryParse(input, out var ret);
                if (parseSuccess)
                {
                    if (ret >= min && ret <= max)
                        return ret;
                }

                Console.WriteLine("잘못된 입력입니다.");
            }
        }

        public class Character // 캐릭터 정보를 저장하는 공간입니다.
        {
            public string Name { get; set; }
            public string Job { get; set; }
            public int Level { get; set; }
            public int Atk { get; set; }
            public int Def { get; set; }
            public int Hp { get; set; }
            public int Gold { get; set; }

            public Character(string name, string job, int level, int atk, int def, int hp, int gold)
            {
                Name = name;
                Job = job;
                Level = level;
                Atk = atk;
                Def = def;
                Hp = hp;
                Gold = gold;
            }
        }
        public class Item // 아이템 정보를 저장하는 공간입니다. 
        {
            public string Name { get; set; }
            public int Atk { get; set; }
            public int Def { get; set; }
            public bool isequipped { get; set; }

            public Item(string name, int atk, int def, bool isequipped)
            {
                Name = name;
                Atk = atk;
                Def = def;
                this.isequipped = isequipped;
            }
        }
    }
}
