# Trivia
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace Trivia
{
    class Question
    {
        public int questionNumber;

        public Question(int questionNumber){
            this.questionNumber = questionNumber;
        }

        public String getTrivia()
        {
            string[] TriviaLines = File.ReadAllLines("TriviaQuestions.txt");
            string[] ListOfAnswers = File.ReadAllLines("ListOfAnswers.txt");

            String str = "Question: " + TriviaLines[questionNumber] + "\r\n";

            Boolean[] alreadyPicked = new Boolean[4];

            Random random = new Random();
            for (int i = 0; i < 4; i++)
            {
                str += "Choice " + (i + 1) + ": ";
                int number;
                do
                {
                    number = random.Next(4);
                }
                while (alreadyPicked[number] == true);

                alreadyPicked[number] = true;

                str += ListOfAnswers[questionNumber * 4 + number] + "\r\n";
            }

            return str;
        }

        public String getRightAnswer()
        {
            string[] ListOfAnswers = File.ReadAllLines("ListOfAnswers.txt");
            return ListOfAnswers[questionNumber * 4 + 0];
        }
    }
}
