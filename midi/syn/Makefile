########################################
#  This file was generated by hdlmake  #
#  http://ohwr.org/projects/hdl-make/  #
########################################

PROJECT := midi.xise
ISE_CRAP := *.b midi_summary.html *.tcl midi.bld midi.cmd_log *.drc midi.lso *.ncd midi.ngc midi.ngd midi.ngr midi.pad midi.par midi.pcf midi.prj midi.ptwx midi.stx midi.syr midi.twr midi.twx midi.gise $(PROJECT).gise midi.bgn midi.unroutes midi.ut midi.xpi midi.xst midi_bitgen.xwbt midi_envsettings.html midi_guide.ncd midi_map.map midi_map.mrp midi_map.ncd midi_map.ngm midi_map.xrpt midi_ngdbuild.xrpt midi_pad.csv midi_pad.txt midi_par.xrpt midi_summary.xml midi_usage.xml midi_xst.xrpt usage_statistics_webtalk.html par_usage_statistics.html webtalk.log webtalk_pn.xml run.tcl

#target for performing local synthesis
local: syn_pre_cmd check_tool
		echo "project open $(PROJECT)" > run.tcl
		echo "process run {Generate Programming File} -force rerun_all" >> run.tcl
		/home/james/opt/Xilinx/14.7/ISE_DS/ISE/bin/lin64/xtclsh run.tcl

check_tool:
		

syn_post_cmd: local
		

syn_pre_cmd:
		

#target for cleaing all intermediate stuff
clean:
		rm -f $(ISE_CRAP)
		rm -rf xst xlnx_auto_*_xdb iseconfig _xmsgs _ngo

#target for cleaning final files
mrproper:
		rm -f *.bit *.bin *.mcs

.PHONY: mrproper clean syn_pre_scipt syn_post_cmd local check_tool

USER:=$(HDLMAKE_RSYNTH_USER)#take the value from the environment
SERVER:=$(HDLMAKE_RSYNTH_SERVER)#take the value from the environment
ISE_PATH:=$(HDLMAKE_RSYNTH_ISE_PATH)
R_NAME:=james/midi
PORT:=22

__test_for_remote_synthesis_variables:
ifeq (x$(USER),x)
	@echo "Remote synthesis user is not set.You can set it by editing variable USER in the makefile or setting env. variable HDLMAKE_RSYNTH_USER." && false
endif
ifeq (x$(SERVER),x)
	@echo "Remote synthesis server is not set.You can set it by editing variable SERVER in the makefile or setting env. variable HDLMAKE_RSYNTH_SERVER." && false
endif
ifeq (x$(ISE_PATH),x)
	@echo "Remote synthesis server is not set.You can set it by editing variable ISE_PATH in the makefile or setting env. variable HDLMAKE_RSYNTH_ISE_PATH." && false
endif

CWD := $(shell pwd)

FILES := ../vhdl/midi.ucf \
../vhdl/midi.vhdl \
../vhdl/shift_out.vhdl \
../vhdl/clock_divider.vhdl \
pa.fromNcd.tcl \
midi.xise

#target for running synthesis in the remote location
remote: __test_for_remote_synthesis_variables __send __do_synthesis
__send_back: __do_synthesis
__do_synthesis: __send
__send: __test_for_remote_synthesis_variables

__send:
		ssh $(USER)@$(SERVER) 'mkdir -p $(R_NAME)'
		rsync -e 'ssh -p $(PORT)' -Ravl $(foreach file, $(FILES), $(shell readlink -f $(file))) $(USER)@$(SERVER):$(R_NAME)

__do_synthesis:
ifeq (x$(HDLMAKE_RSYNTH_USE_SCREEN), x1)
		ssh -t $(USER)@$(SERVER) 'screen bash -c "cd $(R_NAME)$(CWD) && $(HDLMAKE_RSYNTH_ISE_PATH)/xtclsh run.tcl"'
else
		ssh $(USER)@$(SERVER) 'cd $(R_NAME)$(CWD) && $(HDLMAKE_RSYNTH_ISE_PATH)/xtclsh run.tcl'
endif


sync: 
		cd .. && rsync -av $(USER)@$(SERVER):$(R_NAME)/$(CWD) . && cd $(CWD)

#target for removing stuff from the remote location
cleanremote:
		ssh $(USER)@$(SERVER) 'rm -rf $(R_NAME)'

