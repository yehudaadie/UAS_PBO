import java.util.Scanner;

// Kelas Parent Buku
class Buku {
    protected String judul;
    protected int hargaBeli;
    protected int hargaJual;
    protected int stok;

    public Buku(String judul, int hargaBeli, int hargaJual, int stok) {
        this.judul = judul;
        this.hargaBeli = hargaBeli;
        this.hargaJual = hargaJual;
        this.stok = stok;
    }

    public void tambahStok(int jumlah) {
        stok += jumlah;
    }

    public void kurangiStok(int jumlah) {
        if (stok - jumlah >= 0) {
            stok -= jumlah;
        } else {
            System.out.println("Stok tidak mencukupi!");
        }
    }

    public void tampilkanInfo() {
        System.out.println("Judul: " + judul);
        System.out.println("Harga Beli: " + hargaBeli);
        System.out.println("Harga Jual: " + hargaJual);
        System.out.println("Stok: " + stok);
    }
}

// Kelas BukuFiksi turunan dari kelas Buku
class BukuFiksi extends Buku {
    public BukuFiksi(String judul, int hargaBeli, int hargaJual, int stok) {
        super(judul, hargaBeli, hargaJual, stok);
    }
}

// Kelas BukuNonFiksi turunan dari kelas Buku
class BukuNonFiksi extends Buku {
    public BukuNonFiksi(String judul, int hargaBeli, int hargaJual, int stok) {
        super(judul, hargaBeli, hargaJual, stok);
    }
}

// Kelas Majalah turunan dari kelas Buku
class Majalah extends Buku {
    private int nomorEdisi;

    public Majalah(String judul, int hargaBeli, int hargaJual, int stok, int nomorEdisi) {
        super(judul, hargaBeli, hargaJual, stok);
        this.nomorEdisi = nomorEdisi;
    }

    public void tampilkanInfo() {
        super.tampilkanInfo();
        System.out.println("Nomor Edisi: " + nomorEdisi);
    }
}

public class ManajemenPenjualanBuku {
    public static void main(String[] args) {
        int modalAwal = 1000000; // Modal awal
        int modalBerjalan = modalAwal;
        int keuntunganBerjalan = 10000000;

        // Inisialisasi buku
        BukuFiksi bukuFiksi = new BukuFiksi("Malin Kundang", 5000, 10000, 10);
        BukuNonFiksi bukuNonFiksi = new BukuNonFiksi("Astronomi Seru", 6000, 12000, 8);
        Majalah majalah = new Majalah("Lala", 8000, 15000, 5, 1);

        Scanner scanner = new Scanner(System.in);
        int pilihan = 0;

        while (pilihan != 6) {
            System.out.println("************************************");
            System.out.println("Sistem Penjualan Buku");
            System.out.println("By:Yehuda Adi Sucahya,NIM:22201070");
             System.out.println("************************************");
            System.out.println("===== Manajemen Penjualan Buku =====");
            System.out.println("1. Tampilkan Modal Awal dan Keuntungan Berjalan");
            System.out.println("2. Tampilkan Stok Buku");
            System.out.println("3. Penjualan Buku");
            System.out.println("4. Pembelian Buku");
            System.out.println("5. Tampilkan Laporan");
            System.out.println("6. Exit");
            System.out.print("Pilih menu: ");
            pilihan = scanner.nextInt();

            switch (pilihan) {
                case 1:
                    System.out.println("Modal Awal: " + modalAwal);
                    System.out.println("Keuntungan Berjalan: " + keuntunganBerjalan);
                    break;
                case 2:
                    System.out.println("Stok Buku:");
                    bukuFiksi.tampilkanInfo();
                    bukuNonFiksi.tampilkanInfo();
                    majalah.tampilkanInfo();
                    break;
                case 3:
                    System.out.println("=== Penjualan Buku ===");
                    System.out.println("1. Buku Fiksi");
                    System.out.println("2. Buku Non Fiksi");
                    System.out.println("3. Majalah");
                    System.out.print("Pilih jenis buku: ");
                    int jenisBuku = scanner.nextInt();
                    System.out.print("Jumlah buku yang terjual: ");
                    int jumlahTerjual = scanner.nextInt();

                    switch (jenisBuku) {
                        case 1:
                            if (bukuFiksi.stok >= jumlahTerjual) {
                                bukuFiksi.kurangiStok(jumlahTerjual);
                                keuntunganBerjalan += (bukuFiksi.hargaJual - bukuFiksi.hargaBeli) * jumlahTerjual;
                            } else {
                                System.out.println("Stok buku fiksi tidak mencukupi!");
                            }
                            break;
                        case 2:
                            if (bukuNonFiksi.stok >= jumlahTerjual) {
                                bukuNonFiksi.kurangiStok(jumlahTerjual);
                                keuntunganBerjalan += (bukuNonFiksi.hargaJual - bukuNonFiksi.hargaBeli) * jumlahTerjual;
                            } else {
                                System.out.println("Stok buku non fiksi tidak mencukupi!");
                            }
                            break;
                        case 3:
                            if (majalah.stok >= jumlahTerjual) {
                                majalah.kurangiStok(jumlahTerjual);
                                keuntunganBerjalan += (majalah.hargaJual - majalah.hargaBeli) * jumlahTerjual;
                            } else {
                                System.out.println("Stok majalah tidak mencukupi!");
                            }
                            break;
                        default:
                            System.out.println("Pilihan tidak valid!");
                            break;
                    }
                    break;
                case 4:
                    System.out.println("=== Pembelian Buku ===");
                    System.out.println("1. Buku Fiksi");
                    System.out.println("2. Buku Non Fiksi");
                    System.out.println("3. Majalah");
                    System.out.print("Pilih jenis buku: ");
                    jenisBuku = scanner.nextInt();
                    System.out.print("Jumlah buku yang dibeli: ");
                    int jumlahBeli = scanner.nextInt();

                    switch (jenisBuku) {
                        case 1:
                            int totalHargaBeliFiksi = bukuFiksi.hargaBeli * jumlahBeli;
                            if (modalBerjalan >= totalHargaBeliFiksi) {
                                bukuFiksi.tambahStok(jumlahBeli);
                                modalBerjalan -= totalHargaBeliFiksi;
                            } else {
                                System.out.println("Modal tidak mencukupi!");
                            }
                            break;
                        case 2:
                            int totalHargaBeliNonFiksi = bukuNonFiksi.hargaBeli * jumlahBeli;
                            if (modalBerjalan >= totalHargaBeliNonFiksi) {
                                bukuNonFiksi.tambahStok(jumlahBeli);
                                modalBerjalan -= totalHargaBeliNonFiksi;
                            } else {
                                System.out.println("Modal tidak mencukupi!");
                            }
                            break;
                        case 3:
                            int totalHargaBeliMajalah = majalah.hargaBeli * jumlahBeli;
                            if (modalBerjalan >= totalHargaBeliMajalah) {
                                majalah.tambahStok(jumlahBeli);
                                modalBerjalan -= totalHargaBeliMajalah;
                            } else {
                                System.out.println("Modal tidak mencukupi!");
                            }
                            break;
                        default:
                            System.out.println("Pilihan tidak valid!");
                            break;
                    }
                    break;
                case 5:
                    System.out.println("Laporan:");
                    System.out.println("Modal Awal: " + modalAwal);
                    System.out.println("Modal Berjalan: " + modalBerjalan);
                    System.out.println("Keuntungan Berjalan: " + keuntunganBerjalan);
                    break;
                case 6:
                    System.out.println("Terima kasih!");
                    break;
                default:
                    System.out.println("Pilihan tidak valid!");
                    break;
            }

            System.out.println();
        }
    }
}
