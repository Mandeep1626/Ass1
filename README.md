using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading;
using System.Threading.Tasks;

namespace Assignment1
{ 
        class Pet
        {
            public string Name { get; set; }
            public string Type { get; set; }
            public int Hunger { get; set; }
            public int Happiness { get; set; }
            public int Health { get; set; }

            public Pet(string name, string type)
            {
                Name = name;
                Type = type;
                Hunger = 5;
                Happiness = 5;
                Health = 5;
            }

            public void Feed()
            {
                Hunger = Math.Max(0, Hunger - 2);
                Health = Math.Min(10, Health + 1);
                Console.WriteLine($"{Name} has been fed. Hunger decreased, health increased.");
            }

            public void Play()
            {
                if (Hunger >= 8)
                {
                    Console.WriteLine($"{Name} is too hungry to play.");
                }
                else
                {
                    Happiness = Math.Min(10, Happiness + 2);
                    Hunger = Math.Min(10, Hunger + 1);
                    Console.WriteLine($"{Name} is playing. Happiness increased, hunger increased slightly.");
                }
            }

            public void Rest()
            {
                Health = Math.Min(10, Health + 2);
                Happiness = Math.Max(0, Happiness - 1);
                Console.WriteLine($"{Name} is resting. Health increased, happiness decreased slightly.");
            }

            public void CheckStatus()
            {
                Console.WriteLine($"{Name}'s Stats:");
                Console.WriteLine($"Hunger: {Hunger}/10");
                Console.WriteLine($"Happiness: {Happiness}/10");
                Console.WriteLine($"Health: {Health}/10");

                if (Hunger >= 8)
                    Console.WriteLine("Warning: Hunger is critically high.");
                if (Happiness <= 2)
                    Console.WriteLine("Warning: Happiness is critically low.");
                if (Health <= 2)
                    Console.WriteLine("Warning: Health is critically low.");
            }

            public void PassTime()
            {
                Hunger = Math.Min(10, Hunger + 1);
                Happiness = Math.Max(0, Happiness - 1);

                if (Hunger == 10)
                {
                    Health = Math.Max(0, Health - 2);
                    Console.WriteLine($"{Name} is suffering due to extreme hunger. Health decreased.");
                }

                if (Happiness == 0)
                {
                    Health = Math.Max(0, Health - 1);
                    Console.WriteLine($"{Name} is extremely unhappy. Health decreased.");
                }
            }
        }

        class Program
        {
            static void Main(string[] args)
            {
                Console.WriteLine("Welcome to Virtual Pet!");
                Console.WriteLine("Please select a pet type (cat, dog, rabbit):");
                string type = Console.ReadLine();
                Console.WriteLine("Enter your pet's name:");
                string name = Console.ReadLine();

                Pet myPet = new Pet(name, type);
                Console.WriteLine($"Welcome, {myPet.Type} {myPet.Name}!");

                bool exit = false;
                while (!exit)
                {
                    Console.Clear();
                    myPet.CheckStatus();
                    Console.WriteLine("\nChoose an action:");
                    Console.WriteLine("1. Feed");
                    Console.WriteLine("2. Play");
                    Console.WriteLine("3. Rest");
                    Console.WriteLine("4. Check Status");
                    Console.WriteLine("5. Simulate Time Passing");
                    Console.WriteLine("6. Exit");

                    int choice;
                    if (!int.TryParse(Console.ReadLine(), out choice))
                    {
                        Console.WriteLine("Invalid choice. Please enter a number.");
                        continue;
                    }

                    switch (choice)
                    {
                        case 1:
                            myPet.Feed();
                            break;
                        case 2:
                            myPet.Play();
                            break;
                        case 3:
                            myPet.Rest();
                            break;
                        case 4:
                            myPet.CheckStatus();
                            break;
                        case 5:
                            myPet.PassTime();
                            break;
                        case 6:
                            exit = true;
                            break;
                        default:
                            Console.WriteLine("Invalid input !");
                            break;
                    }

                    Thread.Sleep(2000); 
                }
            }
        }
    }

