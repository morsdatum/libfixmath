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

Export('scr_file')
Export('env')
Export('src_dir')
Export('cm0_dir')
Export('cm3_dir')
Export('cm4_dir')
Export('cm4f_dir')

env.SConscript(src_dir+scr_file)

Clean('depend.d',Glob(src_dir+'*.d')
		+Glob(src_dir+cm0_dir+'*/*.d')
		+Glob(src_dir+cm3_dir+'*/*.d')
		+Glob(src_dir+cm4_dir+'*/*.d')
		+Glob(src_dir+cm4f_dir+'*/*.d'))

