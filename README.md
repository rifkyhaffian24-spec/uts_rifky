# Nama: (Rifky Haffian Fasa)
# NIM: (245410042)

⸻

## 1. Teorema CAP dan BASE

### A. Teorema CAP

Teorema CAP menyatakan bahwa dalam sistem terdistribusi kita hanya bisa mendapatkan dua dari tiga hal berikut secara bersamaan:
	•	Consistency (C) – semua node memiliki data yang sama pada waktu yang sama
	•	Availability (A) – sistem selalu merespons permintaan
	•	Partition Tolerance (P) – sistem tetap berjalan meski ada gangguan jaringan

Karena network partition pasti terjadi, maka sistem harus memilih antara:
	•	CP → konsisten, tapi kadang tidak tersedia
	•	AP → tersedia, tapi konsistensinya tertunda

⸻

### B. BASE

BASE adalah pendekatan sistem yang mengutamakan Availability (AP).
	•	Basically Available
	•	Soft-State
	•	Eventual Consistency

BASE digunakan oleh sistem yang memilih Availability + Partition Tolerance.

⸻
### C. Keterkaitan CAP & BASE
	•	Sistem AP → tidak bisa strong consistency
	•	BASE adalah solusi → memberi eventual consistency
	•	Jadi BASE adalah implementasi prinsip CAP pada sistem AP

⸻

### D. Contoh nyata

Saya pernah menggunakan MongoDB.
MongoDB termasuk sistem AP sehingga:
	•	lebih mengutamakan availability
	•	menggunakan mekanisme eventual consistency sesuai prinsip BASE

## 2. GraphQL dan Komunikasi Antar Proses (IPC)

### A. Penjelasan

Dalam sistem terdistribusi, banyak microservice berjalan terpisah (IPC).
GraphQL bisa menjadi gateway yang menghubungkan berbagai proses/microservice.

GraphQL:
	•	menerima 1 query dari client
	•	membuat request ke beberapa service (REST, gRPC, dll)
	•	menggabungkan jawabannya menjadi 1 response

Artinya GraphQL tidak menggantikan IPC, tapi mengkoordinasikan komunikasi antar proses.

### B.Diagram Komunikasi
graph TD

    C(Consistency)
    A(Availability)
    P(Partition<br>Tolerance)

    C -->|Memilih 2| CP[CP System]
    P --> CP
    A -->|Memilih 2| AP[AP System]
    P --> AP
    C -->|Memilih 2| CA[CA System (Tidak Mungkin Saat Partition)]
'''mermaid
flowchart LR
    Client --> GraphQL
    GraphQL --> ServiceA
    GraphQL --> ServiceB
    GraphQL --> ServiceC
'''
