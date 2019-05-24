# Small-game
Small Game - Paper/Scissors/Rock


using System;
using System.Threading;


namespace GRa
{
    class Program
    {
        public enum Choices
        {
            Rock = 0,
            Paper = 1,
            Scissors = 2,
        }

        static int[,] results = new int[3, 3]{
            {0, -1, 1},
            {1, 0, -1},
            {-1, 1, 0},
        };

        static Choices UserChoice_1()
        {
            string input;
            Choices Choice;
            Console.WriteLine("Wybierz:\n(R)ock\n(P)paper\n(S)cissors");

            input = Console.ReadLine().ToUpper();
            if (!(input == "R" || input == "P" || input == "S"))
            {
                Console.WriteLine("Podaj poprawna litere");
                Console.ReadKey();
                Console.Clear();
                UserChoice_1();
                Console.Clear();
            }
            switch (input)
            {
                case "R": Choice = Choices.Rock; break;
                case "P": Choice = Choices.Paper; break;
                default:
                case "S": Choice = Choices.Scissors; break;
            }
            Console.WriteLine(Enum.GetName(typeof(Choices), Choice));
            return Choice;

        }
        static Choices UserChoice_2()
        {
            string input;
            Choices Choice;

            Console.WriteLine("Wybierz:\n(R)ock\n(P)paper\n(S)cissors");

            input = Console.ReadLine().ToUpper();
            if (!(input == "R" || input == "P" || input == "S"))
            {
                Console.WriteLine("Podaj poprawna litere");
                Console.ReadKey();
                Console.Clear();
                UserChoice_2();
                Console.Clear();
            }
                switch (input)
                {
                    case "R": Choice = Choices.Rock; break;
                    case "P": Choice = Choices.Paper; break;
                    default:
                    case "S": Choice = Choices.Scissors; break;
                }
                       
                Console.WriteLine(Enum.GetName(typeof(Choices), Choice));

                return Choice;
        }

        static Choices AiChoice()
        {
            Choices AiChoice;
            Random rnd = new Random();
            AiChoice = (Choices)(rnd.Next(0, 2));
            Console.WriteLine(Enum.GetName(typeof(Choices), AiChoice));
            return AiChoice;
        }

        static void Score_1()
        {
            Choices user = UserChoice_1();
            CoundDown();
            Choices ai = AiChoice();
            switch (results[(int)user, (int)ai])
            {
                case 1: Console.WriteLine("WIN"); break;
                case 0: Console.WriteLine("DRAW"); break;
                case -1: Console.WriteLine("LOSE"); break;
            }
            Console.ReadKey();
            Console.Clear();
        }
        static void Score_2()
        {
            Choices user = UserChoice_1();
            Console.Clear();
            Choices user2 = UserChoice_2();

            switch (results[(int)user, (int)user2])
            {
                case 1: Console.WriteLine("WIN"); break;
                case 0: Console.WriteLine("DRAW"); break;
                case -1: Console.WriteLine("LOSE"); break;
            }
            Console.ReadKey();
            Console.Clear();

        }
        static void Menu()
        {
            int mode;
            string input;
            Console.WriteLine("Choose GameMode \n1.You vs. Ai\n2.You vs Your Friend\n3.Exit.");
            input = Console.ReadLine();
            int.TryParse(input, out mode);


            switch (mode)
            {
                case 1:
                    Score_1();
                    Menu();
                    break;
                case 2:
                    Score_2();
                    Menu();
                    break;
                case 3:
                    Environment.Exit(0);
                    break;
                default:
                    Console.Clear();
                    Menu();
                    break;
            }
        }

        static void CoundDown()
        {
            for (int i = 0; i < 3; i++)
            {
                Console.WriteLine(i + 1);
                Thread.Sleep(100);
            }
        }
        static void Main(string[] args)
        {
            Console.WriteLine("Hi!\nLet's play a game!\n(press enter)");
            Console.ReadKey();
            Console.Clear();
            Menu();
            Console.ReadKey();
            Console.Clear();
            Console.ReadKey();
        }
    }
}
