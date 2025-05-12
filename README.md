class Task:
    def __init__(self, description, category="General", priority="Medium"):
        self.description = description
        self.is_done = False
        self.category = category
        self.priority = priority

    def mark_done(self):
        self.is_done = True

    def __str__(self):
        status = "[x]" if self.is_done else "[ ]"
        return f"{status} {self.description} (Category: {self.category}, Priority: {self.priority})"


class ToDoList:
    def __init__(self):
        self.tasks = []

    def add_task(self, desc, cat=None, prio=None):
        # Using default values if user skips inputs
        category = cat if cat else "General"
        priority = prio if prio else "Medium"
        new_task = Task(desc, category, priority)
        self.tasks.append(new_task)
        print("Task added.")

    def show_tasks(self):
        if not self.tasks:
            print("Nothing to do. Woo!")
        else:
            for idx, task in enumerate(self.tasks):
                print(f"{idx+1}. {task}")

    def complete_task(self, index):
        try:
            self.tasks[index - 1].mark_done()
            print("Marked as complete.")
        except IndexError:
            print("Hmm. That task number doesn't exist.")

    def delete_task(self, index):
        try:
            deleted = self.tasks.pop(index - 1)
            print(f"Removed: {deleted.description}")
        except:
            print("Oops. Invalid task number.")

    def edit_task(self, index, new_desc):
        try:
            self.tasks[index - 1].description = new_desc
            print("Task updated.")
        except:
            print("Couldn't update task. Try again.")


# Note: Just a basic interaction loop here.
def main():
    todo = ToDoList()
    print("Simple To-Do App (type 'help' for commands)")

    while True:
        cmd = input(">> ").strip().lower()
        
        if cmd == "add":
            desc = input("Task description: ")
            cat = input("Category (optional): ")
            prio = input("Priority (Low/Medium/High): ")
            todo.add_task(desc, cat, prio)
        
        elif cmd == "list":
            todo.show_tasks()
        
        elif cmd == "done":
            try:
                idx = int(input("Task number to mark complete: "))
                todo.complete_task(idx)
            except ValueError:
                print("Please enter a number.")
        
        elif cmd == "delete":
            try:
                idx = int(input("Task number to delete: "))
                todo.delete_task(idx)
            except:
                print("Bad input.")
        
        elif cmd == "edit":
            try:
                idx = int(input("Task number to edit: "))
                new_desc = input("New description: ")
                todo.edit_task(idx, new_desc)
            except:
                print("Error editing task.")
        
        elif cmd == "help":
            print("Commands: add, list, done, delete, edit, quit")
        
        elif cmd == "quit":
            print("Goodbye!")
            break
        else:
            print("Unknown command. Try again.")


if __name__ == "__main__":
    main()

OUTPUT:
Simple To-Do App (type 'help' for commands)
>> add
Task description: Buy groceries
Category (optional): Shopping
Priority (Low/Medium/High): High
Task added.
>> add
Task description: Read a book
Category (optional): 
Priority (Low/Medium/High): 
Task added.
>> list
1. [ ] Buy groceries (Category: Shopping, Priority: High)
2. [ ] Read a book (Category: General, Priority: Medium)
>> done
Task number to mark complete: 1
Marked as complete.
>> list
1. [x] Buy groceries (Category: Shopping, Priority: High)
2. [ ] Read a book (Category: General, Priority: Medium)
>> edit
Task number to edit: 2
New description: Read 'Atomic Habits'
Task updated.
>> list
1. [x] Buy groceries (Category: Shopping, Priority: High)
2. [ ] Read 'Atomic Habits' (Category: General, Priority: Medium)
>> delete
Task number to delete: 1
Removed: Buy groceries
>> list
1. [ ] Read 'Atomic Habits' (Category: General, Priority: Medium)
>> quit
Goodbye!