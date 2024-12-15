# tuananh
import tkinter as tk
from tkcalendar import DateEntry
import csv
from datetime import datetime
from tkinter import messagebox


danh_sach_nhan_vien = []


def ghi_du_lieu_csv(du_lieu):
    try:
        with open('du_lieu_nhan_vien.csv', mode='a', newline='', encoding='utf-8') as file:
            writer = csv.writer(file)
            writer.writerow(du_lieu)
    except Exception as e:
        messagebox.showerror("Lỗi", f"Có lỗi xảy ra khi ghi dữ liệu: {e}")


def gui_du_lieu():
    ma_nhan_vien = txtC.get().strip()
    ten_nhan_vien = txtD.get().strip()
    ngay_sinh = txtE.get_date() if txtE.get_date() else None
    gioi_tinh = giới_tính.get()
    don_vi = txtF.get().strip()
    cccd = txtG.get().strip()
    ngay_cap = txtH.get_date() if txtH.get_date() else None
    chuc_danh = txtI.get().strip()
    noi_cap = txtK.get().strip()


    if not (ma_nhan_vien and ten_nhan_vien and ngay_sinh and gioi_tinh and don_vi and cccd and ngay_cap and chuc_danh and noi_cap):
        messagebox.showwarning("Cảnh báo", "Vui lòng điền đầy đủ thông tin!")
        return


    du_lieu = [ma_nhan_vien, ten_nhan_vien, str(ngay_sinh), gioi_tinh, don_vi, cccd, str(ngay_cap), chuc_danh, noi_cap]
    ghi_du_lieu_csv(du_lieu)


    danh_sach_nhan_vien.append((ten_nhan_vien, ngay_sinh))


    messagebox.showinfo("Thông báo", "Dữ liệu đã được ghi thành công!")

    # Làm trống các ô nhập liệu
    txtC.delete(0, tk.END)
    txtD.delete(0, tk.END)
    txtF.delete(0, tk.END)
    txtG.delete(0, tk.END)
    txtI.delete(0, tk.END)
    txtK.delete(0, tk.END)
    giới_tính.set("")
    txtE.set_date(datetime.today())
    txtH.set_date(datetime.today())


def kiem_tra_sinh_nhat():
    today = datetime.today().date()
    sinh_nhat_hom_nay = [ten for ten, sinh_nhat in danh_sach_nhan_vien if datetime.strptime(sinh_nhat, '%Y-%m-%d').date() == today]

    if sinh_nhat_hom_nay:
        messagebox.showinfo("Danh sách sinh nhật hôm nay", "\n".join(sinh_nhat_hom_nay))
    else:
        messagebox.showinfo("Danh sách sinh nhật hôm nay", "Không có ai sinh nhật hôm nay.")


def hien_thi_danh_sach_sinh_nhat():
    today = datetime.today().date()
    sinh_nhat_hom_nay = [ten for ten, sinh_nhat in danh_sach_nhan_vien if datetime.strptime(sinh_nhat, '%Y-%m-%d').date() == today]

    if sinh_nhat_hom_nay:
        danh_sach = "\n".join(sinh_nhat_hom_nay)
        messagebox.showinfo("Danh sách sinh nhật hôm nay", danh_sach)
    else:
        messagebox.showinfo("Danh sách sinh nhật hôm nay", "Không có ai sinh nhật hôm nay.")


giaodien = tk.Tk()
giaodien.title('Thông Tin Nhân Viên')
giaodien.geometry("600x400")


infor = tk.Label(giaodien, text='Thông tin nhân viên', font=("Helvetica", 16))
infor.place(x=15, y=5)


txtA = tk.Checkbutton(giaodien, text='Là khách hàng')
txtA.place(x=130, y=5)


txtB = tk.Checkbutton(giaodien, text='Là nhà cung cấp')
txtB.place(x=250, y=5)


ma = tk.Label(giaodien, text='Mã')
ma.place(x=5, y=35)

txtC = tk.Entry(giaodien)
txtC.place(x=5, y=60, width=80)

# Tên nhân viên
ma1 = tk.Label(giaodien, text='Tên')
ma1.place(x=100, y=35)

txtD = tk.Entry(giaodien)
txtD.place(x=100, y=60, width=150)


ma2 = tk.Label(giaodien, text='Ngày sinh')
ma2.place(x=290, y=35)

txtE = DateEntry(giaodien, width=12, background='darkblue', foreground='white', borderwidth=2, date_pattern='dd/mm/yyyy')
txtE.place(x=290, y=60)

# Giới tính
ma3 = tk.Label(giaodien, text='Giới tính')
ma3.place(x=430, y=35)

# Tạo nút chọn giới tính
giới_tính = tk.StringVar()

radio_nam = tk.Radiobutton(giaodien, text="Nam", variable=giới_tính, value="Nam")
radio_nam.place(x=430, y=60)

radio_nữ = tk.Radiobutton(giaodien, text="Nữ", variable=giới_tính, value="Nữ")
radio_nữ.place(x=490, y=60)

# Đơn vị
donvi = tk.Label(giaodien, text='Đơn Vị')
donvi.place(x=5, y=85)

txtF = tk.Entry(giaodien)
txtF.place(x=5, y=105, width=245)

# Số CCCD
cccd = tk.Label(giaodien, text='Số CCCD')
cccd.place(x=290, y=85)

txtG = tk.Entry(giaodien)
txtG.place(x=290, y=105, width=200)

# Ngày cấp (DateEntry)
ngaycap = tk.Label(giaodien, text='Ngày cấp')
ngaycap.place(x=500, y=85)

txtH = DateEntry(giaodien, width=12, background='darkblue', foreground='white', borderwidth=2, date_pattern='dd/mm/yyyy')
txtH.place(x=500, y=105)

# Chức danh
chucdanh = tk.Label(giaodien, text='Chức danh')
chucdanh.place(x=5, y=130)

txtI = tk.Entry(giaodien)
txtI.place(x=5, y=150, width=245)

# Nơi cấp
noicap = tk.Label(giaodien, text='Nơi cấp')
noicap.place(x=290, y=130)

txtK = tk.Entry(giaodien)
txtK.place(x=290, y=150, width=310)

# Nút gửi dữ liệu
btn_gui = tk.Button(giaodien, text="Gửi", command=gui_du_lieu)
btn_gui.place(x=250, y=180)


# Nút hiển thị danh sách sinh nhật hôm nay
btn_danh_sach_sinh_nhat = tk.Button(giaodien, text="Danh sách sinh nhật hôm nay", command=hien_thi_danh_sach_sinh_nhat)
btn_danh_sach_sinh_nhat.place(x=250, y=260)

# Khởi chạy giao diện
giaodien.mainloop()
