# library--management-systedef add_member():
    name = input("Member name: ").strip()
    class_name = input("Class/section: ").strip()
    phone = input("Phone (optional): ").strip()

    if not name:
        print("Member name cannot be blank.")
        return

    with connect() as con:
        con.execute("""
            INSERT INTO members
            (name, class_name, phone)
            VALUES (?, ?, ?)
        """, (name, class_name, phone))

    print("Member registered successfully.")


def view_members():
    with connect() as con:
        rows = con.execute("""
            SELECT member_id, name, class_name, phone
            FROM members
            ORDER BY name
        """).fetchall()

    if not rows:
        print("No members registered.")
    else:
        for row in rows:
            print(row)m-
