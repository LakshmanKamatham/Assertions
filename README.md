# Assertions
Assertion example

event ev_O_NSCLR;
always @(a_rb_oreg_sclr_val_out or oreg_data_nsclr or a_o_nsclr_gate) begin
               #1ps;
               -> ev_O_NSCLR;
end

property O_NSCLR; 
   
   @(ev_O_NSCLR iff (1)) disable iff (0 || (fmgpio_reg_tb.dut.xio_ioereg_top.gpio_wrapper_0.gpio_reg.xinv_nceout.dout == 1))
   (a_o_nsclr_gate === 1'b1) |-> (oreg_data_nsclr) ===  (a_rb_oreg_sclr_val_out); 
endproperty 
 
        O_NSCLR_check: assert property(O_NSCLR) else $fatal;
