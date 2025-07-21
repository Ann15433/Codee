class Person:
    def __init__(self, name, surname):
        self.name = name
        self.surname = surname

class Reviewer(Person):
    def __str__(self):
        return f"Имя: {self.name}\n" \
               f"Фамилия: {self.surname}"

class Lecturer(Person):
    def __init__(self, name, surname):
        super().__init__(name, surname)
        self.lecture_grades = []
    
    def __str__(self):
        average = sum(self.lecture_grades) / len(self.lecture_grades) if self.lecture_grades else 0
        return f"Имя: {self.name}\n" \
               f"Фамилия: {self.surname}\n" \
               f"Средняя оценка за лекции: {average:.1f}"
    
    def __eq__(self, other):
        if not isinstance(other, Lecturer):
            return NotImplemented
        return sum(self.lecture_grades) / len(self.lecture_grades) == \
               sum(other.lecture_grades) / len(other.lecture_grades)
    
    def __lt__(self, other):
        if not isinstance(other, Lecturer):
            return NotImplemented
        return sum(self.lecture_grades) / len(self.lecture_grades) < \
               sum(other.lecture_grades) / len(other.lecture_grades)
    
    def __le__(self, other):
        return self < other or self == other

class Student(Person):
    def __init__(self, name, surname):
        super().__init__(name, surname)
        self.grades = []
        self.courses_in_progress = []
        self.finished_courses = []
    
    def __str__(self):
        average = sum(self.grades) / len(self.grades) if self.grades else 0
        courses_in_progress = ', '.join(self.courses_in_progress)
        finished_courses = ', '.join(self.finished_courses)
        return f"Имя: {self.name}\n" \
               f"Фамилия: {self.surname}\n" \
               f"Средняя оценка за домашние задания: {average:.1f}\n" \
               f"Курсы в процессе изучения: {courses_in_progress}\n" \
               f"Завершенные курсы: {finished_courses}"
    
    def __eq__(self, other):
        if not isinstance(other, Student):
            return NotImplemented
        return sum(self.grades) / len(self.grades) == \
               sum(other.grades) / len(other.grades)
    
    def __lt__(self, other):
        if not isinstance(other, Student):
            return NotImplemented
        return sum(self.grades) / len(self.grades) < \
               sum(other.grades) / len(other.grades)
    
    def __le__(self, other):
        return self < other or self == other

reviewer = Reviewer("Some", "Buddy")
print(reviewer)

lecturer = Lecturer("Some", "Buddy")
lecturer.lecture_grades = [9, 10, 9, 10]
print(lecturer)

student = Student("Ruoy", "Eman")
student.grades = [9, 10, 9]
student.courses_in_progress = ["Python", "Git"]
student.finished_courses = ["Введение в программирование"]
print(student)

lecturer2 = Lecturer("Other", "Buddy")
lecturer2.lecture_grades = [8, 9, 8]
print(lecturer == lecturer2)  # False
print(lecturer > lecturer2)   # True

student2 = Student("Another", "Student")
student2.grades = [9, 9, 9]
print(student == student2)    # False
print(student > student2)     # True
