# ตรวจสอบวงเล็บในสตริง

ฟังก์ชัน `bracket_check` นี้เป็นฟังก์ชันที่ใช้ในการตรวจสอบวงเล็บที่เปิดและปิดในสตริง ว่ามีคู่ตรงกันหรือไม่ และรายงานข้อผิดพลาดถ้ามีความผิดพลาดในการวางวงเล็บ ฟังก์ชันนี้ทำงานด้วยการใช้โครงสร้างของ stack.


## ฟังก์ชั่น bracket_check()

    ```python
    def bracket_check(test_string):
      #ค่าเริ่มต้น
      stack = Stack()
      is_error = False
      location = []
      i = 0 #ค่า i แทนตำแหน่ง index
      opening_brackets = "({["  # ตัวอักษรที่เป็นวงเล็บที่เปิด
      closing_brackets = ")}]"  # ตัวอักษรที่เป็นวงเล็บที่ปิด
      bracket_pairs = {')': '(', '}': '{', ']': '['} #จับคู่วงเล็บ ถ้าไม่ใช่คู่กัน จะผิด

      #วนลูปตัวอักษรใน test_string
      for char in test_string:

         #ถ้าเป็นวงเล็บเปิดให้เข้าลูปนี้
        if char in opening_brackets:
          stack.push((char,i)) # push วงเล็บเปิดและตำแหน่งเข้าไปในstack


        #ถ้าเป็นวงเล็บปิดให้เข้าลูปนี้
        elif char in closing_brackets:

          #ถ้าstackว่าง แสดงว่าวงเล็บปิดมาก่อน ให้เข้าลูปนี้
          if stack.isEmpty():
            is_error = True # เกิดข้อผิดพลาด
            location.append(i) #ใส่ตำแหน่งที่ผิด

          #ถ้าstackไม่ว่างแสดงว่ามีวงเล็บเปิดก่อนหน้าให้ทำการเปรียบเทียบว่าวงเล็บตรงกันมั้ย จาก bracket_pairs
          elif not stack.isEmpty():
            top, top_i = stack.pop() #popทั้งวงเล็บเปิดและค่าindexที่เคย push ไว้ ออกมาใส่ตัวแปร top และ top_i

            # ถ้าวงเล็บที่ปิดไม่ตรงกับวงเล็บที่เปิดที่ push ไว้ ให้เข้าลูปนี้
            if top != bracket_pairs[char]:  #
                        is_error = True  # เกิดข้อผิดพลาด
                        location.append(top_i)  # เพิ่มตำแหน่งข้อผิดพลาดของวงเล็บที่เปิด
                        location.append(i) #เพิ่มตำแหน่งข้อผิดพลาดของวงเล็บที่ปิด


        i+=1  #เพิ่มค่า index ทุกครั้งที่วนลูป


      #เมื่อสิ้นสุด forLoop แล้วถ้า stack ยังไม่ว่างแสดงว่าวงเล็บเปิดยังไม่หมด
      #ให้popมันออกแล้วแสดงข้อผิดพลาด โดยใช้ whileLoop
      while not stack.isEmpty():
          last, last_i = stack.pop() #ใส่วงเล็บเปิดที่คาไว้ และตำแหน่งของตัวนั้น ลงในตัวแปร last , last_i
          is_error = True
          location.append(last_i) #เพิ่มตำแหน่งข้อผิดพลาดของวงเล็บเปิด
      return is_error, location


##วิธีใช้

ในการเรียกใช้ `bracket_check` คุณต้องส่งสตริงที่คุณต้องการตรวจสอบเป็นอาร์กิวเมนต์ ตัวอย่างการใช้งาน:

```python
test_string = "((a + b) * (c - d))"
is_error, location = bracket_check(test_string)
if is_error:
    print("ข้อผิดพลาดในวงเล็บที่ตำแหน่ง:", location)
else:
    print("ไม่มีข้อผิดพลาดในวงเล็บ")

