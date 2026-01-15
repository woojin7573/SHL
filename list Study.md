# SHL
List로 구성된 운송장 CRUD 코드
using System;using System;
using System.Collections.Generic;

namespace Study
{
    class StudyItem
    {
        public string INV_ID { get; set; }
    }

    class Program
    {
        static List<StudyItem> studies = new List<StudyItem>();

        static void Main(string[] args)
        {
            while (true)
            {
                Console.Clear(); 
                Console.WriteLine("운송장 관리 프로그램");
                Console.WriteLine("1.조회");
                Console.WriteLine("2.추가");
                Console.WriteLine("3.수정");
                Console.WriteLine("4.삭제");
                Console.WriteLine("5.종료");
                Console.Write("선택: ");
                var choice = Console.ReadLine();

                switch (choice)
                {
                    case "1":
                        ReadStudy();
                        break;
                    case "2":
                        CreateStudy();
                        break;
                    case "3":
                        UpdateStudy();
                        break;
                    case "4":
                        DeleteStudy();
                        break;
                    case "5":
                        return;
                    default:
                        Console.WriteLine("잘못된 선택입니다. 계속하려면 아무 키나 누르세요...");
                        Console.ReadKey();
                        break;
                }
            }
        }

        static void ReadStudy()
        {
            Console.Clear(); 
            Console.WriteLine("---운송장 목록---");
            if (studies.Count == 0)
            {
                Console.WriteLine("등록된 운송장이 없습니다.");
            }
            else
            {
                int idx = 1;
                foreach (var s in studies)
                {
                    Console.WriteLine($"{idx++}. 운송장 번호: {s.INV_ID}");
                }
            }

            Console.WriteLine();
            Console.WriteLine("메인으로 돌아가려면 아무 키나 누르세요...");
            Console.ReadKey(); 
        }

        static void CreateStudy()
        {
            Console.Clear(); 
            Console.Write("추가할 운송장 번호 입력: ");
            string inv = Console.ReadLine();

            if (string.IsNullOrWhiteSpace(inv))
            {
                Console.WriteLine("입력값이 비어있습니다.");
            }
            else
            {
                studies.Add(new StudyItem { INV_ID = inv });
                Console.WriteLine("추가 완료");
            }

            Console.WriteLine("메인으로 돌아가려면 아무 키나 누르세요...");
            Console.ReadKey();
        }

        static void UpdateStudy()
        {
            Console.Clear(); 
            Console.Write("수정할 운송장 번호: ");
            string oldInv = Console.ReadLine();
            var s = studies.Find(x => x.INV_ID == oldInv);

            if (s != null)
            {
                Console.Write("새 운송장 번호: ");
                string newInv = Console.ReadLine();
                if (string.IsNullOrWhiteSpace(newInv))
                {
                    Console.WriteLine("새 운송장 번호가 비어있습니다.");
                }
                else
                {
                    s.INV_ID = newInv;
                    Console.WriteLine("수정 완료");
                }
            }
            else
            {
                Console.WriteLine("해당 운송장을 찾을 수 없음");
            }

            Console.WriteLine("메인으로 돌아가려면 아무 키나 누르세요...");
            Console.ReadKey();
        }

        static void DeleteStudy()
        {
            Console.Clear(); 
            Console.Write("삭제할 운송장 번호: ");
            string inv = Console.ReadLine();
            var s = studies.Find(x => x.INV_ID == inv);

            if (s != null)
            {
                studies.Remove(s);
                Console.WriteLine("삭제 완료");
            }
            else
            {
                Console.WriteLine("해당 운송장을 찾을 수 없음");
            }

            Console.WriteLine("메인으로 돌아가려면 아무 키나 누르세요...");
            Console.ReadKey();
        }
    }
}
