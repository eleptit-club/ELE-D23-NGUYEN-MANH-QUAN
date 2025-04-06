# moore và mealy

|đặc điểm|moore|mealy|
|---|---|---|
|đầu ra phụ thuộc vào| chỉ trạng thái| cả trạng thái hiện tại và đầu vào|
|phản ứng đầu ra| chậm hơn|nhanh hơn|
|số trạng thái cần thiết|ít hơn|nhiều hơn|
|ứng dụng| cần phản hồi nhanh, như bộ giải mã, điều khuyển trình tự| cần ổn định, như bộ chia tần số, đèn giao thông|

moore
câu 1
code
	module bai1 (
		input clk, rst, a, b, c, d,
		output reg out 
	);
	 [1:0] reg state, n_state;
	 parameter a = 0, b = 1, c = 2, d = 3;
	 always @ (*) begin 
		case(state)
			a: n_state = in ? b:a;
			b: n_state = in ? b:c;
			c: n_state = in ? d:a;
			d: n_state = in ? b:c;
		endcase 
	 end 
	 assign out = (state == d) ? 1:0
	 always @ (posedge clk) begin
		if (rst) state <= a;
		else state <= n_state;
	 end
	endmodule
	
testbench

	module tb_bai1;
		reg clk, rst, a, b, c, d;
		wire out;

		// Gọi module chính
		bai1 uut (
			.clk(clk),
			.rst(rst),
			.a(a),
			.b(b),
			.c(c),
			.d(d),
			.out(out)
		);

		// Tạo xung clock 10ns
		always #5 clk = ~clk;

		initial begin
			// Khởi tạo tín hiệu
			clk = 0; rst = 1;
			a = 0; b = 0; c = 0; d = 0;
			#10; 
			
			rst = 0; // Bỏ reset
			#10;
			
			// Test chuyển trạng thái
			a = 1; #10; a = 0;
			b = 1; #10; b = 0;
			c = 1; #10; c = 0;
			d = 1; #10; d = 0;

			// Kết thúc mô phỏng
			#50;
			$finish;
		end

		initial begin
			$monitor("Time=%0t | clk=%b | rst=%b | a=%b | b=%b | c=%b | d=%b | out=%b", 
					 $time, clk, rst, a, b, c, d, out);
		end

	endmodule
bai 2

code
	module bai2(
		input clk,rst,
		output out
	);
		parameter A=0, B=1;
		reg [1:0]state, nesxt_State;
		
		always @(*)begin
			case(state)	
			A: next_State=in?A:B;
			B: next_State=in?B:A;
		end 
		
		always @(posedge clk) begin
			if(rst) state<=B;
			else state<=next_State;
		end
		
		assign out=(state==B?1:0);
		
	endmodule
	
testbench 
	module tb_bai2;

		reg clk, rst, in;
		wire out;

		bai2 uut (
			.clk(clk),
			.rst(rst),
			.in(in),
			.out(out)
		);

		always #5 clk = ~clk;

		initial begin
			// Khởi tạo tín hiệu
			clk = 0;
			rst = 1;
			in = 0;

			#10;
			rst = 0;

			// Test chuỗi tín hiệu đầu vào
			#10 in = 0;   // từ B -> A (vì đang reset vào B)
			#10 in = 1;   // giữ A
			#10 in = 1;   // giữ A
			#10 in = 0;   // A -> B
			#10 in = 1;   // giữ B
			#10 in = 0;   // B -> A
			#10 in = 0;   // A -> B
			#10 in = 1;   // giữ B

			// Kết thúc mô phỏng
			#20 $finish;
		end

		initial begin
			$monitor("Time = %0t | rst = %b | in = %b | out = %b", $time, rst, in, out);
		end

	endmodule
bài 3
code 
	module bai3(
		input in;
		output out
	);
		parameter A=0, B=1, C=2, D=3;
		reg [2:0]state, nesxt_State;
		
		always @(*)begin
			case(state)	
			A: next_State=in?B:A;
			B: next_State=in?B:C;
			C: next_State=in?D:A;
			D: next_State=in?B:C;
		end 
		
		always @(posedge clk) begin
			if(rst) state<=A;
			else state<=next_State;
		end
		
		assign out=(state==D?1:0);
		
	endmodule

TESTBENCH

	module tb_bai3;

		reg clk, rst, in;
		wire out;

		bai2 uut (
			.clk(clk),
			.rst(rst),
			.in(in),
			.out(out)
		);

		always #5 clk = ~clk;

		initial begin
			// Khởi tạo
			clk = 0;
			rst = 1;
			in = 0;

			#12 rst = 0;

			// Chuỗi tín hiệu kiểm tra
			#10 in = 0;   // B -> C
			#10 in = 1;   // C -> D
			#10 in = 0;   // D -> C
			#10 in = 0;   // C -> A
			#10 in = 1;   // A -> B
			#10 in = 0;   // B -> C
			#10 in = 1;   // C -> D
			#10 in = 1;   // D -> B
			#10 in = 1;   // B -> B
			#10 in = 0;   // B -> C
			#10 in = 0;   // C -> A

			#20 $finish;
		end

		initial begin
			$monitor("Time = %0t | in = %b | state = %0d | out = %b", $time, in, uut.state, out);
		end

	endmodule

	KIỂU MEALY
bài 4
code 
	module bai4(
		input in,rst,clk;
		output out
	);
		parameter idle=0, a=1, b=2;
		reg [2:0]state, next_State;
		always @(*)begin
			case(state)	
			ilde: next_State=in?idle:a;
			a: next_State=in?idle:b;
			b: next_State=in?idle:b;
		end 
		
		always @(posedge clk) begin
			if(rst) state<=idle;
			else state<=next_State;
		end
		
		assign out=(state==b?1:0);
		
	endmodule
	
testbench

	module tb_bai4;

		reg clk, rst, in;
		wire out;

		bai2 uut (
			.clk(clk),
			.rst(rst),
			.in(in),
			.out(out)
		);

		always #5 clk = ~clk;

		initial begin

			clk = 0;
			rst = 1;
			in = 0;

			#10 rst = 0;

			#10 in = 0;   // idle -> a
			#10 in = 0;   // a -> b
			#10 in = 0;   // b -> b
			#10 in = 1;   // b -> idle
			#10 in = 0;   // idle -> a
			#10 in = 1;   // a -> idle
			#10 in = 0;   // idle -> a
			#10 in = 0;   // a -> b
			#10 in = 0;   // b -> b

			#20 $finish;
		end

		initial begin
			$monitor("Time = %0t | in = %b | state = %0d | out = %b", $time, in, uut.state, out);
		end

	endmodule

baid 5
code
	module bai5(
		input in,clk,rst;
		output out
	);
		parameter  a=0, b=1;
		reg [1:0]state, next_State;
		always @(*)begin
			case(state)	
			a: next_State=in?b:a;
			b: next_State=in?b:b;
		end 
		
		always @(posedge clk) begin
			if(rst) state<=a;
			else state<=next_State;
		end
		
		assign out=(state==b?1:0);
		
	endmodule
	
testbench

	module tb_bai5;

		reg clk, rst, in;
		wire out;

		bai4 uut (
			.clk(clk),
			.rst(rst),
			.in(in),
			.out(out)
		);

		always #5 clk = ~clk;

		initial begin

			clk = 0;
			rst = 1;
			in = 0;

			#12 rst = 0;

			#10 in = 0;  // giữ a
			#10 in = 1;  // a -> b
			#10 in = 0;  // giữ b
			#10 in = 1;  // giữ b
			#10 in = 0;  // giữ b
			#10 rst = 1; // reset lại về a
			#10 rst = 0;
			#10 in = 0;  // giữ a
			#10 in = 1;  // a -> b

			#20 $finish;
		end

		initial begin
			$monitor("Time = %0t | in = %b | state = %0d | out = %b", $time, in, uut.state, out);
		end

	endmodule

bai 6
code
	module bai6(
		input in,clk,rst;
		output out
	);
		parameter  a=0, b=1, c=2;
		reg [2:0]state, next_State;
		always @(*)begin
			case(state)	
			a: next_State=in?b:a;
			b: next_State=in?b:c;
			c: next_State=in?b:a
		end 
		
		always @(posedge clk) begin
			if(rst) state<=a;
			else state<=next_State;
		end
		
		assign out=(state==c?1:0);
		
	endmodule
	
testbench

	module tb_bai6;

		reg clk, rst, in;
		wire out;

		bai6 uut (
			.clk(clk),
			.rst(rst),
			.in(in),
			.out(out)
		);

		always #5 clk = ~clk;

		initial begin

			clk = 0;
			rst = 1;
			in = 0;

			#10 rst = 0;

			#10 in = 1;  // a -> b
			#10 in = 0;  // b -> c
			#10 in = 0;  // c -> a
			#10 in = 1;  // a -> b
			#10 in = 1;  // b -> b
			#10 in = 0;  // b -> c
			#10 in = 1;  // c -> b
			#10 in = 0;  // b -> c
			#10 in = 0;  // c -> a

			#10 rst = 1;
			#10 rst = 0;

			#10 in = 1;  // a -> b
			#10 in = 0;  // b -> c

			#20 $finish;
		end

		initial begin
			$monitor("Time = %0t | in = %b | state = %0d | out = %b", $time, in, uut.state, out);
		end

	endmodule

