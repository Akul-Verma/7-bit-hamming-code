# 7-bit-hamming-code
module hamming(O,A);
input [6:0] A;
output [7:0] O;
wire[2:0] W;
wire [7:0]D;
xor(W[0],A[0],A[2],A[4],A[6]);
xor(W[1],A[1],A[2],A[5],A[6]);
xor(W[2],A[3],A[4],A[5],A[6]);
decoder dd(D,W);
buf(O[0],D[0]);
xor(O[1],D[1],A[0]);
xor(O[2],D[2],A[1]);
xor(O[3],D[3],A[2]);
xor(O[4],D[4],A[3]);
xor(O[5],D[5],A[4]);
xor(O[6],D[6],A[5]);
xor(O[7],D[7],A[6]);
endmodule
module decoder(O,I);
input [2:0] I;
output [7:0] O;
wire [3:0] N;
not(N[0],I[0]);
not(N[1],I[1]);
not(N[2],I[2]);
and(O[0],N[2],N[1],N[0]);
and(O[1],N[2],N[1],I[0]);
and(O[2],N[2],I[1],N[0]);
and(O[3],N[2],I[1],I[0]);
and(O[4],I[2],N[1],N[0]);
and(O[5],I[2],N[1],I[0]);
and(O[6],I[2],I[1],N[0]);
and(O[7],I[2],I[1],I[0]);
endmodule
module hamming_tb();
reg [6:0] a;
 wire[7:0] o;
 hamming f1(.O(o),.A(a));
 initial
 begin
 $monitor($time,"a=%b,o=%b",a,o);
 a=7'b1001001;
 #10
 a=7'b1001011;
 #10
 a=7'b1101001;
 end
endmodule
