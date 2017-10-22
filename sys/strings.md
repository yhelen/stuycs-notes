_9/27_

# Aim: ctrings

Strings
    Strings are character arrays.

    By convention, strings end with a null character.
        (either '' or 0 or '\0')

    When you make a literal string using "", an immutable string
    is created in memory. These strings are automatically null terminated.

    All references to the same literal string refer to the same
    immutable string in memory.

    Declaring String

        char s0[256];
            Normal array declaration, allocating 256 bytes

        char s1[256] = "Imagine";
            Allocates 256 bytes.
            Creates immutable string "Imagine" and then copies it
            (including the terminating null) into the array.

        char s2[] = "Tuesday";
            Allocates 8 bytes. (appropriate to assignment)
            Creates the immutable string "Tuesday" and then copies it.

        char *s3 = "Mankind";
            Creates the immutable string "Mankind" and return a pointer to
            that string.
            Since the pointer is to an immutable piece of memory, you cannot
            modify strings created in this way.

        You can only assign char arrays with = at declaration
            char s[] = "zero";
            s = "seven"; // NOT OK! arrays are immutable pointers

        Char pointers can be assigned using = at any time
            char *s = "zero";
            s = "seven"; // ok!

Recommended use of string n fxns:
strncpy(s1, s2, sizeof(s1) - 1);
strncat(s1, s2, sizeof(s1) - strlen(s2))
