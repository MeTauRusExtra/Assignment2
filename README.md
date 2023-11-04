# ฟังก์ชั่นตรวจสอบข้อผิดพลาดของวงเล็บ
    
'def bracket_check(test_string):
  1.stack = Stack()
  2.is_error = False
  3.location = []
  4.i = 0 #ค่า i แทนตำแหน่ง index
  opening_brackets = "({["  # ตัวอักษรที่เป็นวงเล็บที่เปิด
  closing_brackets = ")}]"  # ตัวอักษรที่เป็นวงเล็บที่ปิด
  bracket_pairs = {')': '(', '}': '{', ']': '['} #จับคู่วงเล็บ ถ้าไม่ใช่คู่กัน จะผิด'

  **วนลูปตัวอักษรใน test_string**
  for char in test_string:
    **ถ้าเป็นวงเล็บเปิดให้เข้าลูปนี้**
    if char in opening_brackets:
      stack.push((char,i)) ----- *push วงเล็บเปิดและตำแหน่งเข้าไปในstack*
    **ถ้าเป็นวงเล็บปิดให้เข้าลูปนี้**
    elif char in closing_brackets:
      *ถ้าstackว่าง แสดงว่าวงเล็บปิดมาก่อน ให้เข้าลูปนี้*
      if stack.isEmpty():
        is_error = True  
        location.append(i) ----- *ใส่ตำแหน่งวงเล็บปิดที่ผิด*
      **ถ้าstackไม่ว่างแสดงว่ามีวงเล็บเปิดก่อนหน้าให้ทำการเปรียบเทียบว่าวงเล็บตรงกันมั้ย จาก bracket_pairs**
      elif not stack.isEmpty():
        top, top_i = stack.pop() ----- *popทั้งวงเล็บเปิดและค่าindexที่เคย push ไว้ ออกมาใส่ตัวแปร top และ top_i*
        **ถ้าวงเล็บที่ปิดไม่ตรงกับวงเล็บที่เปิดที่ push ไว้ ให้เข้าลูปนี้**
        if top != bracket_pairs[char]:  #
                    is_error = True  
                    location.append(top_i) ----- *เพิ่มตำแหน่งข้อผิดพลาดของวงเล็บที่เปิด*
                    location.append(i) ----- *เพิ่มตำแหน่งข้อผิดพลาดของวงเล็บที่ปิด*

    ## เพิ่มค่า index ที่ครั้งที่วนลูป1รอบ
    i+=1  

  ## เมื่อสิ้นสุด forLoop แล้วถ้า stack ยังไม่ว่างแสดงว่าวงเล็บเปิดยังไม่หมด
  ## ให้popมันออกแล้วแสดงข้อผิดพลาด โดยใช้ whileLoop
  while not stack.isEmpty():
      last, last_i = stack.pop() ----- *ใส่วงเล็บเปิดที่คาไว้ และตำแหน่งของตัวนั้น ลงในตัวแปร last , last_i*
      is_error = True
      location.append(last_i) ------ *เพิ่มตำแหน่งข้อผิดพลาดของวงเล็บเปิด*

      
  return is_error, location '
  
  ### ค่า location ของตำแหน่งวงเล็บที่ผิดพลาดที่ได้จากฟังชั่นก์ bracket_check()นี้บางกรณีอาจจะไม่ได้จัดเรียง
  ### เนื่องจากถ้ามีวงเล็บเปิดซ้อนกันมากๆ ในwhileLoopจะpopเอาตำแหน่งของตัวที่มาหลังก่อนดังนั้นเราสามารถจัดเรียงค่าlocationหลังจากเข้าลูปนี้


![alt text](image.jpg)
  
