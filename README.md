class Reviewer:
    def __init__(self, name, surname):
        self.name = name
        self.surname = surname
    
    def __str__(self):
        return f'Имя: {self.name}\nФамилия: {self.surname}'

class Lecturer:
    def __init__(self, name, surname):
        self.name = name
        self.surname = surname
        self.grades = []
    
    def __str__(self):
        average_grade = sum(self.grades) / len(self.grades)
        return f'Имя: {self.name}\nФамилия: {self.surname}\nСредняя оценка за лекции: {average_grade:.1f}'

    def __eq__(self, other):
        return sum(self.grades) / len(self.grades) == sum(other.grades) / len(other.grades)

    def __lt__(self, other):
        return sum(self.grades) / len(self.grades) < sum(other.grades) / len(other.grades)

    # Остальные операторы сравнения...

class Student:
    def __init__(self, name, surname):
        self.name = name
        self.surname = surname
        self.grades = []
        self.courses_in_progress = []
        self.finished_courses = []
    
    def __str__(self):
        average_grade = sum(self.grades) / len(self.grades)
        return f'Имя: {self.name}\nФамилия: {self.surname}\nСредняя оценка за домашние задания: {average_grade:.1f}\nКурсы в процессе изучения: {", ".join(self.courses_in_progress)}\nЗавершенные курсы: {", ".join(self.finished_courses)}'

    def rate_lecturer(self, lecturer, course, grade):
        if isinstance(lecturer, Lecturer) and course in lecturer.courses_attached and course in self.courses_in_progress:
            lecturer.grades.append(grade)
        else:
            return 'Ошибка'

    def __eq__(self, other):
        return sum(self.grades) / len(self.grades) == sum(other.grades) / len(other.grades)

    def __lt__(self, other):
        return sum(self.grades) / len(self.grades) < sum(other.grades) / len(other.grades)

    # Остальные операторы сравнения...

# Пример использования:

# Создаем преподавателя
some_lecturer = Lecturer('Some', 'Buddy')

# Создаем студента
some_student = Student('Ruoy', 'Eman')

# Выставляем оценку лектору
some_student.rate_lecturer(some_lecturer, 'Python', 9)
some_student.rate_lecturer(some_lecturer, 'Python', 10)
some_student.rate_lecturer(some_lecturer, 'Python', 8)

# Выводим информацию о лекторе и студенте
print(some_lecturer)
print(some_student)


