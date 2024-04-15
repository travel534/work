class Student:
  def __init__(self, name, surname, gender):
    self.name = name
    self.surname = surname
    self.gender = gender
    self.finished_courses = []
    self.courses_in_progress = []
    self.courses_attached = []
    self.grades = {}

  def rate_hw(self, lecturer, course, grade):
    if isinstance(lecturer, Lecturer) and course in lecturer.courses_attached:
      if course in lecturer.grades:
        lecturer.grades[course] += [grade]
      else:
        lecturer.grades[course] = [grade]
    else:
      return 'Ошибка'

  def average_rate(self):
      total_grades = 0
      total_courses = 0
      for grades_list in self.grades.values():
          total_grades += sum(grades_list)
          total_courses += len(grades_list)
      if total_grades > 0:
          return round(total_grades / total_courses, 1)

      else:
          return 0

  def __str__(self):

      some_student = f'Имя: {self.name}\n'\
      f'Фамилия: {self.surname}\n'\
      f'Средняя оценка за домашние задания: {self.average_rate()}\n'\
      f'Курсы в процессе изучения: {", ".join(self.courses_in_progress)}\n'\
      f'Завершенные курсы: {", ".join(self.finished_courses)}\n'
      return some_student
    
  def __gt__(self, other):
      return self.average_rate() > other.average_rate()

class Mentor:

  def __init__(self, name, surname):
    self.name = name
    self.surname = surname
    self.courses_attached = []


class Lecturer(Mentor):
  grades = {}
  def __init__(self, name, surname):
    super().__init__(name,surname)
    self.grades = {}
    
  def average_rate(self):
     
     total_grades = 0
     total_courses = 0
     for grades_list in self.grades.values():
         total_grades += sum(grades_list)
         total_courses += len(grades_list)
     if total_grades > 0:
         return round(total_grades / total_courses, 1)

     else:
         return 0
       
  def __str__(self):
    some_lecturer = f'Имя: {self.name}\n'\
    f'Фамилия: {self.surname}\n'\
    f'средняя оценка за лекции: {self.average_rate()}\n'
    return some_lecturer
    
  def __gt__(self, other):
      return self.average_rate() > other.average_rate()

class Reviewer(Mentor):

  def rate_hw(self, student, course, grade):
    if isinstance(student, Student) and \
    course in self.courses_attached and \
    course in student.courses_in_progress:
      if course in student.grades:
        student.grades[course] += [grade]
      else:
        student.grades[course] = [grade]
    else:
      return 'Ошибка'

  def __str__(self):
    some_reviewer = f'Имя: {self.name}\n'\
    f'Фамилия: {self.surname}\n'
    return some_reviewer


best_student = Student('Ruoy', 'Eman', 'your_gender')
best_student.courses_in_progress += ['Python']

best_lecturer = Lecturer('Some', 'Buddy')
best_lecturer.courses_attached += ['Python']

best_reviewer = Reviewer('Some', 'Buddy')
best_reviewer.courses_attached += ['Python']
Reviewer.rate_hw(best_reviewer, best_student, 'Python', 10)
Reviewer.rate_hw(best_reviewer, best_student, 'Python', 10)
Reviewer.rate_hw(best_reviewer, best_student, 'Python', 10)

best_student.courses_attached += ['Python']
best_student.rate_hw(best_lecturer, 'Python', 10)
best_student.rate_hw(best_lecturer, 'Python', 10)
best_student.rate_hw(best_lecturer, 'Python', 10)


print(best_student.grades)
print(best_lecturer.grades)



some_reviewer = Reviewer('Some', 'Buddy')
some_lecturer = Lecturer('Some', 'Buddy' )
some_student = Student('Ruoy', 'Eman','your_gender')

some_student.courses_in_progress += ['Python']
some_student.courses_in_progress += ['Git']
some_student.finished_courses += ['Введение в программирование']

some_lecturer.courses_attached += ['Python']
some_lecturer.courses_attached += ['Git']
some_student.rate_hw(some_lecturer, 'Python', 10)
some_student.rate_hw(some_lecturer, 'Python', 10)
some_student.rate_hw(some_lecturer, 'Python', 10)
some_student.rate_hw(some_lecturer, 'Git', 10)
some_student.rate_hw(some_lecturer, 'Git', 10)
some_student.rate_hw(some_lecturer, 'Git', 10)
some_student.rate_hw(some_lecturer, 'Git', 9)


some_reviewer.courses_attached += ['Python']
some_reviewer.courses_attached += ['Git']
some_reviewer.rate_hw(some_student, 'Python', 10)
some_reviewer.rate_hw(some_student, 'Python', 10)
some_reviewer.rate_hw(some_student, 'Python', 10)
some_reviewer.rate_hw(some_student, 'Git', 10)
some_reviewer.rate_hw(some_student, 'Git', 10)
some_reviewer.rate_hw(some_student, 'Git', 10)
some_reviewer.rate_hw(some_student, 'Git', 9)


some_lecturer_2 = Lecturer('Eddy', 'Bobby')
some_lecturer_2.courses_attached += ['Python']
some_lecturer_2.courses_attached += ['Git']

some_student.rate_hw(some_lecturer_2, 'Python', 10)
some_student.rate_hw(some_lecturer_2, 'Python', 10)
some_student.rate_hw(some_lecturer_2, 'Python', 5)
some_student.rate_hw(some_lecturer_2, 'Git', 10)
some_student.rate_hw(some_lecturer_2, 'Git', 10)
some_student.rate_hw(some_lecturer_2, 'Git', 10)



some_student_2 = Student('Ric', 'Lee','your_gender')
some_student_2.courses_in_progress += ['Python']
some_student_2.courses_in_progress += ['Git']
some_student_2.finished_courses += ['Введение в программирование']

some_reviewer.courses_attached += ['Python']
some_reviewer.courses_attached += ['Git']
some_reviewer.rate_hw(some_student_2, 'Python', 10)
some_reviewer.rate_hw(some_student_2, 'Python', 10)
some_reviewer.rate_hw(some_student_2, 'Python', 7)
some_reviewer.rate_hw(some_student_2, 'Git', 10)
some_reviewer.rate_hw(some_student_2, 'Git', 10)
some_reviewer.rate_hw(some_student_2, 'Git', 10)
some_reviewer.rate_hw(some_student_2, 'Git', 10)


print(some_reviewer)
print(some_lecturer)
print(some_lecturer_2)
print(some_student)
print(some_student_2)
#print(some_student > some_student_2)
#print(some_lecturer > some_lecturer_2)

if some_lecturer < some_lecturer_2:
  print(f'{some_lecturer_2.name}, {some_lecturer_2.surname}'
    f' преподают лучше чем {some_lecturer.name}, {some_lecturer.surname}.')
else:
  print(f'{some_lecturer.name}, {some_lecturer.surname} преподают лучше, чем '
    f'{some_lecturer_2.name}, {some_lecturer_2.surname}.')

if some_student < some_student_2:
  print(f'{some_student_2.name}, {some_student_2.surname}'
    f' учатся лучше, чем {some_student.name}, {some_student.surname}.')
else:
  print(f'{some_student.name, some_student.surname} учатся лучше, чем '
    f'{some_student_2.name}, {some_student_2.surname}.')

# 4 задание


lec_list = [some_lecturer, some_lecturer_2]
stud_list = [some_student, some_student_2]
def student_rating(stud_list, course_name):
    sum_all = 0
    count = 0       
    for stud in stud_list:
        for course_name in stud.grades:
            if course_name != course_name:
                return stud.grades.values()
             
            sum_all += sum(stud.grades[course_name])
            count += len(stud.grades[course_name]) 
    if sum_all > 0:
        return round(sum_all / count, 1)   
    else:
        return 0
  
        

def lecturer_rating(lec_list, course_name):
  sum_all = 0
  count = 0
  for lec in lec_list:
    for course_name in lec.grades:
        if course_name != course_name:
            return lec.grades.values()
            
        sum_all += sum(lec.grades[course_name])
        count += len(lec.grades[course_name]) 
  if count > 0:
    return round(sum_all / count, 1)   
  else:
    return 0
  
  
print()
print(f"Средняя оценка для всех студентов по курсу {'Python'}: "
  f"{student_rating(stud_list, 'Python')}")

print(f"Средняя оценка для всех лекторов по курсу {'Python'}: "
f"{lecturer_rating(lec_list, 'Python')}")
