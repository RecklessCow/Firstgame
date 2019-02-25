using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Threading;




namespace Snakeeee
{

    class main
    {
        public static void Main()
        {
            Console.ForegroundColor = ConsoleColor.Yellow;
            gameobject main = new gameobject();
            while (true)
            {
                Thread.Sleep(100);
                Console.Clear();
                main.createboard.Boardprint();
                main.snakecreate();
                main.negr();
                if (main.posx2 == main.posx && main.posy2 == main.posy)
                {
                    break;
                }
            }
            Console.Clear();
            Console.WriteLine("you wooon!!1!");
            Console.ReadKey();
        }

    }

    class gameobject
    {
        Random rnd = new Random();
        public GameBoard createboard = new GameBoard(20, 20);

        public int posx; public int posx2;
        public int posy; public int posy2;

        public gameobject()
        {
            posx = rnd.Next(0, createboard.height);
            posy = rnd.Next(0, createboard.width);
            posx2 = rnd.Next(0, createboard.height);
            posy2 = rnd.Next(0, createboard.width);
        }
        
        public void negr()
        {
            createboard.board[posx2, posy2] = 4;
        }

        public void snakecreate()
        {

            Array.Clear(createboard.board, 0, createboard.board.Length);
            try
            {
                ConsoleKey command = Console.ReadKey().Key;

                switch (command)
                {
                    case ConsoleKey.NumPad8:
                        posx--;
                        break;
                    case ConsoleKey.NumPad5:
                        posx++;
                        break;
                    case ConsoleKey.NumPad6:
                        posy++;
                        break;
                    case ConsoleKey.NumPad4:
                        posy--;
                        break;
                }
                createboard.board[posx, posy] = 1;
            }
            catch (IndexOutOfRangeException)
            {
                if(posy > createboard.height - 1)
                {
                    posy = posy - createboard.height - 1;
                }
                else if (posx > createboard.width - 1)
                {
                    posx = posx - createboard.width - 1;
                }
                else if (posy < 0)
                {
                    posy = posy + createboard.height + 1;
                }
                else if (posx < 0)
                {
                    posx = posx + createboard.width + 1;
                }
            }
        }
    }


    public class GameBoard
    {
        public int width;
        public int height;

        public int[,] board;

        public GameBoard(int Hwidth, int Vheight)
        {
            width = Hwidth;
            height = Vheight;

            board = new int[Hwidth, Vheight];
        }

        public void Boardprint()
        {

            for (int w = 0; w < width; w++)
            {
                for (int h = 0; h < height; h++)
                {
                    Console.Write(board[w, h] + " ");
                }
                Console.WriteLine();
            }
            Console.WriteLine();

        }


    }

}
