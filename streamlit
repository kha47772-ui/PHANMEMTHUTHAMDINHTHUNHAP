
import streamlit as st

# Cấu hình trang
st.set_page_config(
    page_title="Tính chỉ số DTI",
    page_icon="🏦",
    layout="centered"
)

st.title("🏦 TÍNH CHỈ SỐ DTI")
st.write("Đánh giá khả năng vay vốn của khách hàng")

st.divider()

# 1. Nhập thông tin khách hàng
st.subheader("Nhập thông tin khách hàng")

STV = st.number_input(
    "Số tiền vay (VNĐ)",
    min_value=1_000_000,
    value=800_000_000,
    step=10_000_000
)

THV = st.number_input(
    "Thời hạn vay (năm)",
    min_value=1,
    value=5,
    step=1
)

LS = st.number_input(
    "Lãi suất vay (%/năm)",
    min_value=0.0,
    value=12.0,
    step=0.5
)

TN = st.number_input(
    "Thu nhập hàng tháng (VNĐ)",
    min_value=0,
    value=45_000_000,
    step=1_000_000
)

NC = st.number_input(
    "Nợ cũ phải trả hàng tháng (VNĐ)",
    min_value=0,
    value=10_000_000,
    step=1_000_000
)

CPSH = st.number_input(
    "Chi phí sinh hoạt mỗi người/tháng (VNĐ)",
    min_value=0,
    value=4_000_000,
    step=500_000
)

SN = st.number_input(
    "Số người trong gia đình",
    min_value=1,
    value=3,
    step=1
)

# 2. Tính toán khi nhấn nút
if st.button("TÍNH DTI", type="primary",
              use_container_width=True):

    # Đổi lãi suất % thành số thập phân
    lai_suat = LS / 100

    # Tính DTI theo công thức ban đầu
    mau_so = TN - CPSH * SN

    if mau_so <= 0:
        st.error(
            "Không thể tính DTI vì thu nhập sau "
            "chi phí sinh hoạt phải lớn hơn 0."
        )

    else:
        DTI = (
            (
                STV / (THV * 12)
                + STV * (lai_suat / 12)
            )
            + NC
        ) / mau_so

        # 3. Hiển thị kết quả
        st.divider()
        st.subheader("Kết quả")

        st.metric(
            label="Chỉ số DTI",
            value=f"{DTI:.2%}"
        )

        st.write("**Ngưỡng đánh giá: 70%**")

        # 4. Kết luận theo yêu cầu
        if DTI < 0.70:
            st.error("❌ KHÔNG ĐƯỢC VAY")
        else:
            st.success("✅ ĐƯỢC VAY")

        # 5. Chi tiết tính toán
        with st.expander("Xem chi tiết"):
            st.write(
                f"Tiền gốc/tháng: "
                f"{STV / (THV * 12):,.0f} VNĐ"
            )

            st.write(
                f"Tiền lãi/tháng: "
                f"{STV * (lai_suat / 12):,.0f} VNĐ"
            )

            st.write(
                f"Tổng nợ hàng tháng: "
                f"{STV / (THV * 12) + STV * "
                f"(lai_suat / 12) + NC:,.0f} VNĐ"
            )

            st.write(
                f"Chi phí sinh hoạt gia đình: "
                f"{CPSH * SN:,.0f} VNĐ"
            )

            st.write(
                f"Thu nhập còn lại: {mau_so:,.0f} VNĐ"
            )

st.divider()
st.caption(
    "Kết quả được xác định theo công thức và "
    "ngưỡng DTI do người dùng thiết lập."
)
