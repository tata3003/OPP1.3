class Student:
    def __init__(self, name, surname, gender):
        self.name = name
        self.surname = surname
        self.gender = gender
        self.finished_courses = []
        self.courses_in_progress = []
        self.grades = {}

    def rate_lecture(self, lecturer, course, grade):
        if isinstance(lecturer, Lecturer) and course in lecturer.courses_attached and course in self.courses_in_progress:
            if course in lecturer.grades:
                lecturer.grades[course] += [grade]
            else:
                lecturer.grades[course] = [grade]
        else:
            return 'Ошибка'

class Mentor:
    def __init__(self, name, surname):
        self.name = name
        self.surname = surname
        self.courses_attached = []

    def rate_hw(self, student, course, grade):
        if isinstance(student, Student) and course in self.courses_attached and course in student.courses_in_progress:
            if course in student.grades:
                student.grades[course] += [grade]
            else:
                student.grades[course] = [grade]
        else:
            return 'Ошибка'

class Lecturer(Mentor):
    def __init__(self, name, surname):
        super().__init__(name, surname)
        self.grades = {}

    def average_grade(self):
        sum_grades = 0
        count_grades = 0
        for grades_list in self.grades.values():
            sum_grades += sum(grades_list)
            count_grades += len(grades_list)
        return sum_grades / count_grades if count_grades != 0 else 0

class Reviewer(Mentor):
    def __init__(self, name, surname):
        super().__init__(name, surname)

    def rate_hw(self, student, course, grade):
        super().rate_hw(student, course, grade)

# Пример использования классов:

# Создаем лектора и студента
lecturer = Lecturer('Иван', 'Иванов')
student = Student('Петр', 'Петров', 'м')

# Добавляем лектору курс
lecturer.courses_attached.append('Python')

# Добавляем студенту курс
student.courses_in_progress.append('Python')

# Выставляем оценку лектору
student.rate_lecture(lecturer, 'Python', 8)

# Выводим оценку лектора
print(f'Средняя оценка лектора {lecturer.name} {lecturer.surname}: {lecturer.average_grade()}')

# Создаем ревьюера и выставляем оценку студенту
reviewer = Reviewer('Алексей', 'Сидоров')
reviewer.rate_hw(student, 'Python', 9)

# Выводим оценки студента
print(f'Оценки студента {student.name} {student.surname} по курсу {student.courses_in_progress[0]}: {student.grades}')


