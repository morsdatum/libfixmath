# Top SConstruct file

tool_path = '/opt/freddie-arm-5_3/'
cross_prefix = tool_path+'bin/arm-none-eabi-'

cc_flags = Split('''
		-Wall -Wextra 
		-ffunction-sections -fdata-sections 
		-fno-common -MD 
		''')
cxx_flags = Split('''
		-x c++ -pipe
		-Wall -Wextra -Winline
		-Wcast-align -Wcast-qual -Wshadow
		-fno-exceptions -fno-rtti
		-ffunction-sections -fdata-sections
		-funsigned-bitfields -fshort-enums
		-pedantic -MD
		''')
	
as_flags = Split('-x assembler-with-cpp -Wa,-ahlms=$(<:.s=.lst),--gstabs -MD -D_ASSEMBLER_ -mthumb')

ld_flags = Split('''
		-Wall
		--static
		-nostartfiles
		-Wl,--gc-sections
		''')

ar_flags=Split('rcs')

opti_flags = Split('-O3 -fomit-frame-pointer -fexpensive-optimizations -g')

cm0_dir = 'build_cortex_m0plus/'
cm3_dir = 'build_cortex_m3/'
cm4_dir = 'build_cortex_m4/'
cm4f_dir = 'build_cortex_m4f/'
src_dir ='libfixmath/'
scr_file = 'SConscript'


env = Environment(
			CCFLAGS=cc_flags+opti_flags,
			CC=cross_prefix+'gcc',
			CXXFLAGS=cxx_flags+opti_flags,
			CXX=cross_prefix+'gcc',
			LINKFLAGS=ld_flags,
			LINK=cross_prefix+'gcc',
			ASFLAGS=as_flags+opti_flags,
			AS=cross_prefix+'gcc',
			CPPPATH=Split(src_dir+' '+tool_path+'/arm-none-eabi/include'),
			AR=cross_prefix+'ar',
			ARFLAGS=ar_flags,
			RANLIB=cross_prefix+'ranlib'
		)


cm0_sw = Split('-mcpu=cortex-m0plus -mfloat-abi=soft -mthumb')
cm0_env = env.Clone()
cm0_env.Append(CCFLAGS=cm0_sw,CXXFLAGS=cm0_sw,LINKFLAGS=cm0_sw,ASFLAGS=cm0_sw)

cm3_sw = Split('-mcpu=cortex-m3 -mfloat-abi=soft -mthumb')
cm3_env = env.Clone()
cm3_env.Append(CCFLAGS=cm3_sw,CXXFLAGS=cm3_sw,LINKFLAGS=cm3_sw,ASFLAGS=cm3_sw)

cm4_sw = Split('-mcpu=cortex-m4 -mfloat-abi=soft -mfpu=fpv4-sp-d16 -mthumb')
cm4_env = env.Clone()
cm4_env.Append(CCFLAGS=cm4_sw,CXXFLAGS=cm4_sw,LINKFLAGS=cm4_sw,ASFLAGS=cm4_sw)

cm4f_sw = Split('-mcpu=cortex-m4 -mfloat-abi=hard -mfpu=fpv4-sp-d16 -mthumb')
cm4f_env = env.Clone()
cm4f_env.Append(CCFLAGS=cm4f_sw,CXXFLAGS=cm4f_sw,LINKFLAGS=cm4f_sw,ASFLAGS=cm4f_sw)



env.SConscript(src_dir+scr_file, exports={'env':cm0_env, 'cm_sw':'M0plus'}, variant_dir=cm0_dir, duplicate=0)
env.SConscript(src_dir+scr_file, exports={'env':cm3_env, 'cm_sw':'M3'}, variant_dir=cm3_dir, duplicate=0)
env.SConscript(src_dir+scr_file, exports={'env':cm4_env, 'cm_sw':'M4'} , variant_dir=cm4_dir,duplicate=0)
env.SConscript(src_dir+scr_file, exports={'env':cm4f_env, 'cm_sw':'M4F'}, variant_dir=cm4f_dir,duplicate=0)

Clean('depend.d',Glob(src_dir+'*.d')
		+Glob(cm0_dir+'*/*.d')
		+Glob(cm3_dir+'*/*.d')
		+Glob(cm4_dir+'*/*.d')
		+Glob(cm4f_dir+'*/*.d'))

