class SmartToDo:
    def __init__(self):
        self.tasks = []

    def add_task(self, task, due_date=None):
        self.tasks.append({"task": task, "done": False, "due_date": due_date})

    def view_tasks(self):
        for i, t in enumerate(self.tasks, start=1):
            status = "✅ Done" if t["done"] else "❌ Pending"
            print(f"{i}. {t['task']} (Due: {t['due_date']}) - {status}")

    def complete_task(self, index):
        if 0 <= index < len(self.tasks):
            self.tasks[index]["done"] = True
            print(f"Task '{self.tasks[index]['task']}' marked as done ✅")
        else:
            print("Invalid task number!")

    def ai_suggest_task(self):
        """Simple AI: Suggests task with 'urgent' or nearest due date"""
        if not self.tasks:
            return "No tasks available!"
        
        # Priority by keyword
        for t in self.tasks:
            if not t["done"] and "urgent" in t["task"].lower():
                return f"AI Suggestion: Do this task first 👉 {t['task']}"
        
        # Priority by due date
        pending = [t for t in self.tasks if not t["done"] and t["due_date"]]
        if pending:
            # earliest due date
            pending.sort(key=lambda x: x["due_date"])
            return f"AI Suggestion: Next task 👉 {pending[0]['task']} (Due {pending[0]['due_date']})"
        
        return "AI Suggestion: Finish any pending task."

# ----------------------------
# Example Usage
# ----------------------------
todo = SmartToDo()
todo.add_task("Finish AI project report - urgent", "2025-09-30")
todo.add_task("Buy groceries", "2025-09-25")
todo.add_task("Read SDLC notes")

print("\n📌 All Tasks:")
todo.view_tasks()

print("\n🤖 AI Suggestion:")
print(todo.ai_suggest_task())

print("\n✅ Completing Task 2...")
todo.complete_task(1)

print("\n📌 Updated Task List:")
todo.view_tasks()

print("\n🤖 AI Suggestion:")
print(todo.ai_suggest_task())


