
#include <stdio.h>
#include <string.h>

int main() {
    FILE *fp;
    int n, i;
    char name[100];
    char age[20];
    char course[100];
    char line[200];

    printf("Writing Student Database:\n");
    printf("How many students do you want to record? ");
    scanf("%d", &n);
    getchar();

    fp = fopen("/tmp/student_records.txt", "w");

    if (fp == NULL) {
        perror("Error opening file");
        return 1;
    }

    for (i = 1; i <= n; i++) {
        printf("\nStudent %d\n", i);

        printf("Enter Name: ");
        fgets(name, sizeof(name), stdin);
        name[strcspn(name, "\n")] = '\0';

        printf("Enter Age: ");
        fgets(age, sizeof(age), stdin);
        age[strcspn(age, "\n")] = '\0';

        printf("Enter Course: ");
        fgets(course, sizeof(course), stdin);
        course[strcspn(course, "\n")] = '\0';

        fprintf(fp, "Student %d\n", i);
        fprintf(fp, "Name: %s\n", name);
        fprintf(fp, "Age: %s\n", age);
        fprintf(fp, "Course: %s\n", course);
        fprintf(fp, "____________________\n");
    }

    fclose(fp);

    printf("\nStudent database successfully saved to file.\n");

    fp = fopen("/tmp/student_records.txt", "r");

    if (fp == NULL) {
        perror("Error reading file");
        return 1;
    }

    printf("\nReading Student Database:\n\n");

    while (fgets(line, sizeof(line), fp) != NULL) {
        printf("%s", line);
    }

    fclose(fp);

    return 0;
}
