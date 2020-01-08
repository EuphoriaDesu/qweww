using System;

namespace Perceptron
{
    class Program
    {
        static void Main(string[] args)
        {
            // Количество входных данных, выходные данные
            Perc perceptron = new Perc(10, new int[] {0,1});
            Console.WriteLine(">Входные данные<");
            printIntArray(perceptron.Inputs);
            Console.WriteLine();
            Console.WriteLine(">Начальные весовые коэффиценты<");
            printIntArray(perceptron.Weigths);
            Console.WriteLine();
            perceptron.train();
            Console.WriteLine(">Конечные весовые коэффиценты<");
            printIntArray(perceptron.Weigths);
            Console.WriteLine();
            Console.WriteLine(">Количество итераций - " + perceptron.Iterator + "<");
            Console.ReadLine();
        }
        static void printIntArray(int[] array)
        {
            foreach (int item in array)
            {
                Console.WriteLine(item);
            }
        }
    }

    class Perc
    {
        private int[] inputs;
        private int inputsLength = 10;
        private int[] weigths;
        private int[] outputs;
        private int iterator = 0;

        public int[] Inputs
        {
            get { return inputs; }
        }

        public int[] Weigths
        {
            get { return weigths; }
        }

        public int Iterator
        {
            get { return iterator; }
        }

        public Perc(int inputsLength, int[] outputs)
        {
            this.inputsLength = inputsLength;
            this.inputs = getInputs();
            this.weigths = createWeights();
            this.outputs = outputs;
        }

        public void train()
        {
            int y;
            int u;
            do
            {
                u = summator(inputs, weigths);
                Console.WriteLine("Значение выходной функции: " + u);
                y = getY(u);
                if (y > 1)
                {
                    for (int i = 0; i < inputs.Length; i++)
                    {
                        weigths[i] -= inputs[i];
                    }

                }
                else
                {
                    for (int i = 0; i < inputs.Length; i++)
                    {
                        weigths[i] += inputs[i];
                    }

                }
                iterator++;

            } while (y != 1);

        }

        public int getY(int u)
        {
            if (u >= 0)
            {
                return 1;
            }
            else return 0;
        }

        private int[] getInputs() {
            int[] result = new int[inputsLength];
            for (int i = 0; i < inputsLength; i++)
            {
                result[i] = new Random().Next(-10, 11);
            }
            return result;
        }

        private int[] createWeights()
        {
            int[] result = new int[inputsLength];
            for (int i = 0; i < inputsLength; i++)
            {
                result[i] = new Random().Next(-100, 101);
            }
            return result;
        }

        private int summator(int[] inputs, int[] weights)
        {
            int sum = 0;
            for (int count = 0; count < 10; count++)
            {
                sum += inputs[count] * weights[count];
            }
            return sum;
        }
    }
}
