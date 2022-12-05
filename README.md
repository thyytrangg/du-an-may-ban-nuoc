# du-an-may-ban-nuoc
# Máy bán nước tự động

import datetime
# danh sách

gia = {1: 3000, 2: 5000, 3: 7000, 4: 8000, 5: 10000, 6: 15000, 7: 14000, 8: 20000, 9: 18000}
loai = {1: "1.nước lọc: 3000", 2: "2.tăng lực:5000", 3: "3.sting:7000", 4: "4.O_long: 8000", 5: "5.C2:10000",
        6: "6.cafe sữa:15000", 7: "7.cafe đen:14000", 8: "8.trà sữa lon:20000", 9: "9.bí đao:18000"}
soluong = {1: 10, 2: 10, 3: 10, 4: 10, 5: 10, 6: 10, 7: 10, 8: 10, 9: 10}

# Các hàm

def tien(soluong, dongia):    #chi phí phải trả
    return soluong*dongia

def tienthua(tiennhan, phaitra):  # tiền thừa
    return tiennhan - phaitra

def tienthieu(phaitra, tiennhan):  # tiền thiếu
    return phaitra - tiennhan


print("XIN KÍNH CHÀO QUÝ KHÁCH ĐÃ ĐẾN ZỚI MÁY BÁN NƯỚC TỰ ĐỘNG")
print('---Hãy chọn loại và số lượng nước---')
for x in loai.values():  # in bảng menu = <<dictionary: key.values>>
    print(x)
print('\n')


choice = 1
soTienPhaiTra = 0
tongSoTienPhaiTra = 0
buy = True
while buy == True:
    # Chọn loại nước
    ln = int(input("Chọn loại nước muốn mua: "))
    if ln <= 0 or ln > 9:
        print("Vui lòng chọn đúng mã nước! --> Mời nhập lại")
        continue  # quay lại cho người mua nhập lại loại nước
    # Chọn số lượng
    sl = int(input("Nhập vào số lượng muốn mua: "))
    if sl > soluong[ln]:
        print("Loại nước quý khách chọn chỉ còn:", soluong[ln], "chai/hộp", "\n")
        print("Bạn có muốn mua tiếp không??", "\n", "1 = Có  |  0 = Không ")
        choice = int(input("Lựa chọn của bạn: "))
        if choice == 0:
            print("Kết thúc chương trình")
            break
        if choice == 1:
            sl = int(input("Mời bạn nhập lại số lượng muốn mua: "))

            soluong[ln] = soluong[ln] - sl
            '''công thức trên cập nhật lại số chai nước hiện còn lại trong máy'''

            soTienPhaiTra = tien(sl,gia[ln])
            print("Số tiền phải trả là: ", soTienPhaiTra, "\n")
    else:
        soluong[ln] = soluong[ln] - sl #tương tự ở trên 
        soTienPhaiTra = tien(sl,gia[ln])
        print("Số tiền phải trả là: ", soTienPhaiTra, "\n")
    
    tongSoTienPhaiTra = tongSoTienPhaiTra + soTienPhaiTra                           #tính tổng số tiền 
    print(f"Tổng tiền: {tongSoTienPhaiTra}","\n")

    print("Bạn muốn tiếp tục mua hay thanh toán??", "\n", "1 = Thanh Toán | 2 = Tiếp Tục Mua | 0 = Hủy ")
    choice = int(input("Lựa chọn của bạn: "))
    if choice == 0:
        print("Kết thúc chương trình")
        break  
    if choice == 1:
        print("Mời bạn thanh toán nè!", "\n")
        tienMayNhan = int(input("Số tiền khách hàng cho vào máy: "))
        if tienMayNhan >= tongSoTienPhaiTra:
            tienThua = tienthua(tienMayNhan, tongSoTienPhaiTra)
            print("Tiền thừa: ", tienThua)
            dt1 = datetime.datetime.now()  # thời gian thanh toán thành công
            print("Quý khách đã thanh toán THÀNH CÔNG lúc: ", dt1)
            print("CẢM ƠN VÀ HẸN GẶP LẠI!!!")
            break
        else:
            tienThieu = tienthieu(tongSoTienPhaiTra, tienMayNhan)
            print("Còn thiếu: ", tienThieu)
            i = 1
            while True:  # đợi khi số tiền thiếu = 0
                tienTraThem = int(input(f"Tiền trả thêm {i} : "))
                i += 1
                tienThieu = tienThieu - tienTraThem

                if tienThieu > 0:
                    print(f"Còn thiếu {tienThieu}")

                else:
                    tienThua = 0 - tienThieu
                    print(f"Đã thanh toán đủ tiền. Tiền thừa: {tienThua}")
                    break

            dt1 = datetime.datetime.now()  # thời gian thanh toán thành công
            print("Quý khách đã thanh toán THÀNH CÔNG lúc: ", dt1)
            print("CẢM ƠN VÀ HẸN GẶP LẠI!!!")
            break
    if choice == 2:
        buy = True

