# ─────────────────────────────────────────
#  GPA Calculator
#  Supports Regular, Honors, and AP courses
#  Tracks multiple semesters + cumulative GPA
# ─────────────────────────────────────────

# Weighted GPA boosts
WEIGHTS = {
    "regular": 0.0,
    "honors":  0.5,
    "ap":      1.0
}

# Letter grade to base GPA value
GRADE_POINTS = {
    "A+": 4.0, "A": 4.0, "A-": 3.7,
    "B+": 3.3, "B": 3.0, "B-": 2.7,
    "C+": 2.3, "C": 2.0, "C-": 1.7,
    "D+": 1.3, "D": 1.0, "D-": 0.7,
    "F":  0.0
}


def get_grade_points(grade, course_type):
    """Convert a letter grade + course type to weighted GPA points."""
    grade = grade.upper().strip()
    course_type = course_type.lower().strip()

    if grade not in GRADE_POINTS:
        raise ValueError(f"Invalid grade '{grade}'. Use A, A-, B+, B, etc.")
    if course_type not in WEIGHTS:
        raise ValueError(f"Invalid course type '{course_type}'. Use regular, honors, or ap.")

    return GRADE_POINTS[grade] + WEIGHTS[course_type]


def input_courses():
    """Prompt user to enter courses for one semester. Returns list of weighted points."""
    courses = []
    print("\n  Enter each course below.")
    print("  Course types: regular, honors, ap")
    print("  Grades: A, A-, B+, B, B-, C+, C, etc.")
    print("  Type 'done' when finished.\n")

    while True:
        course_name = input("  Course name (or 'done'): ").strip()
        if course_name.lower() == "done":
            if not courses:
                print("  Please enter at least one course.")
                continue
            break

        grade = input(f"  Grade for {course_name}: ").strip()
        course_type = input(f"  Type for {course_name} (regular/honors/ap): ").strip()

        try:
            points = get_grade_points(grade, course_type)
            courses.append((course_name, grade, course_type, points))
            print(f"  ✓ Added — weighted points: {points:.2f}\n")
        except ValueError as e:
            print(f"  ✗ Error: {e}. Please try again.\n")

    return courses


def calculate_gpa(courses):
    """Calculate GPA from a list of (name, grade, type, points) tuples."""
    if not courses:
        return 0.0
    return sum(c[3] for c in courses) / len(courses)


def display_semester(semester_num, courses, gpa):
    """Print a formatted summary for one semester."""
    print(f"\n  ┌─────────────────────────────────────────┐")
    print(f"  │         Semester {semester_num} Summary               │")
    print(f"  ├──────────────────┬──────┬──────────┬─────┤")
    print(f"  │ Course           │Grade │ Type     │ Pts │")
    print(f"  ├──────────────────┼──────┼──────────┼─────┤")
    for name, grade, ctype, pts in courses:
        print(f"  │ {name[:16]:<16} │ {grade:<4} │ {ctype:<8} │{pts:>4.1f} │")
    print(f"  ├──────────────────┴──────┴──────────┴─────┤")
    print(f"  │  Semester GPA: {gpa:.2f}                       │")
    print(f"  └─────────────────────────────────────────┘")


def main():
    print("=" * 47)
    print("         Weighted GPA Calculator")
    print("=" * 47)

    all_courses = []
    semester_num = 1

    while True:
        print(f"\n── Semester {semester_num} ──────────────────────────────")
        courses = input_courses()
        gpa = calculate_gpa(courses)
        display_semester(semester_num, courses, gpa)
        all_courses.extend(courses)

        # Cumulative so far
        cumulative = calculate_gpa(all_courses)
        print(f"\n  Cumulative GPA after {semester_num} semester(s): {cumulative:.2f}")

        another = input("\n  Add another semester? (yes/no): ").strip().lower()
        if another not in ("yes", "y"):
            break
        semester_num += 1

    # Final summary
    print("\n" + "=" * 47)
    print("              Final Summary")
    print("=" * 47)
    print(f"  Total courses:    {len(all_courses)}")
    print(f"  Total semesters:  {semester_num}")
    print(f"  Cumulative GPA:   {calculate_gpa(all_courses):.2f}")
    print("=" * 47)
    print("\n  Done! Run the script again to start over.\n")


if __name__ == "__main__":
    main()
