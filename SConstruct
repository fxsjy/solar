protoc = Builder(action='thirdparty/bin/protoc --proto_path=./src/protocol/ --cpp_out=./src/protocol/ $SOURCE') 
env_gen = Environment(BUILDERS={'Protoc':protoc})

env_gen.Protoc(['src/protocol/galaxy.pb.h','src/protocol/galaxy.pb.cc'], 'src/protocol/galaxy.proto')
env_gen.Protoc(['src/protocol/resman.pb.h','src/protocol/resman.pb.cc'], 'src/protocol/resman.proto')
env_gen.Protoc(['src/protocol/agent.pb.h','src/protocol/agent.pb.cc'], 'src/protocol/agent.proto')
env_gen.Protoc(['src/protocol/appmaster.pb.h','src/protocol/appmaster.pb.cc'], 'src/protocol/appmaster.proto')


env = Environment(
        CPPPATH = ['.', 'thirdparty/boost_1_57_0/', './thirdparty/include', 'src/utils'] ,
        LIBS = ['sofa-pbrpc', 'protobuf', 'snappy', 'gflags', 'glog', 'tcmalloc_minimal','pthread', 'z', 'rt', 'boost_filesystem'],
        LIBPATH = ['./thirdparty/lib', './thirdparty/boost_1_57_0/stage/lib'],
        CCFLAGS = '-g2 -Wall -Werror ',
        LINKFLAGS = '-Wl,-rpath-link ./thirdparty/boost_1_57_0/stage/lib')

env.Program('resman', Glob('src/resman/*.cc') + Glob('src/utils/*.cc') 
            + ['src/protocol/resman.pb.cc', 'src/protocol/galaxy.pb.cc'])

env.Program('appmaster', Glob('src/appmaster/*.cc') + Glob('src/utils/*.cc')
            + ['src/protocol/appmaster.pb.cc', 'src/protocol/galaxy.pb.cc'])

env.Program('appworker', Glob('src/appworker/*.cc') + Glob('src/utils/*.cc')
            + ['src/protocol/galaxy.pb.cc'])

env.Program('agent', Glob('src/agent/*.cc') + Glob('src/utils/*.cc') + Glob('src/agent/*/*.cc')
            + ['src/protocol/agent.pb.cc', 'src/protocol/galaxy.pb.cc'])



