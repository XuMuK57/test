                Структуры. Типы значений и ссылочные типы
Цель: получить практические навыки в создании программ, содержащих добавление в программу структур. Изучить разницы в поведении типов значений и ссылочных типов. Изучить работу сборщика мусора, а также работы сборщика мусора с использованием пользовательских типов данных. Постановка задачи: изучить соответствующий материал. В данной работе нужно рассмотреть, как добавлять в объектно-ориентированную программу структуры, изучить чем структуры отличаются от классов, изучается на примерах различий в поведениях этих двух типов объектов.
Задание:
1. Выберите любую концепцию, тему или приложение, которое вам интересно разработать в рамках этой лабораторной работы. Это может быть любое приложение, реализующее какую-либо логику (симулятор поиска данных, вычислений, обработка строк и тд). Обязательно убедитесь, что выбранное вами приложение можно логически разделить на компоненты, где одни компоненты будут использовать структуры, а другие - классы.
2. Создайте в своем проекте как минимум одну структуру и один класс, которые будут представлять компоненты вашего приложения.
3. Реализуйте функциональность для работы с этими компонентами, включая их инициализацию, изменение и вывод информации.
4. Реализуйте методы для создания копий экземпляров классов и структур:
4.1. Реализуйте методы, которые будут создавать новые экземпляры классов (копировать их) с изменёнными параметрами.
4.2. Реализуйте методы, которые будут создавать новые экземпляры структур (копировать их) с изменёнными параметрами. Для создания копий экземпляров примените выражение «with».
                  
 5. Протестируйте ваше приложение и убедитесь, что оно работает корректно и демонстрирует различия между значимыми и ссылочными типами.
Ход работы:
Код:
using System;
using System.Collections.Generic;
public class Task {
public int Num { get; set; } public string Heading { get; set; } public string Done { get; set; }
public Task(int num, string heading, string done) {
Num=num; Heading = heading; Done = done;
}
public Task CopyWithNewHeading(string newHeading) {
return new Task(Num, newHeading, Done); }
public Task CopyWithDoneStatus(string DoneStatus) {
return new Task(Num, Heading, DoneStatus); }
public override string ToString() {
return $"Задание No{Num}: {Heading} (Статус: {Done})"; }
}
public struct TaskList {
public List<Task> Tasks { get; set; }
public TaskList(List<Task> tasks) {
Tasks = tasks; }
public TaskList AddTask(Task task) {
  List<Task> newTasks = new List<Task>(Tasks);

newTasks.Add(task);
return new TaskList(newTasks); }
public TaskList RemoveTask(int taskId) {
List<Task> newTasks = new List<Task>(Tasks);
Task taskToRemove = newTasks.Find(t => t.Num == taskId); if (taskToRemove != null)
newTasks.Remove(taskToRemove); return new TaskList(newTasks);
}
public override string ToString() {
string taskListStr = "Список задач:\n"; foreach (var task in Tasks)
{
taskListStr += task.ToString() + "\n"; }
return taskListStr; }
}
class Program {
static void Main() {
Task task1 = new Task(1, "Выгулять собаку", "выполнено"); Task task2 = new Task(2, "Приготовить обед", "не выполнено");
TaskList taskList = new TaskList(new List<Task> { task1, task2 }); Console.WriteLine(taskList);
// Добавляю новую задачу и вывожу список
Task task3 = new Task(3, "Подготовиться к занятию", "не выполнено"); taskList = taskList.AddTask(task3);
Console.WriteLine(taskList);
// Изменяю статус задачи и вывожу список
taskList.Tasks[0] = taskList.Tasks[0].CopyWithDoneStatus("выполнено"); Console.WriteLine(taskList);
// Удаляю задачу и вывожу список taskList = taskList.RemoveTask(1); Console.WriteLine(taskList);
} }


