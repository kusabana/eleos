<div align="center">
  <h3><a href="https://github.com/kusabana">
    ~kusabana/</a>eleos – έ‧λε‧ος ( mercy, compassion )
  </h3>
c++20 header-only library for exposing source engine interfaces
</div>

#
### installation
* cmake
```cmake
# Subdir
add_subdirectory("path/to/eleos")

# FetchContent
FetchContent_Declare(
  eleos
  GIT_REPOSITORY https://github.com/kusabana/eleos.git
  GIT_TAG 1.0.0
)

FetchContent_MakeAvailable(eleos)

# ...

target_link_libraries(library PUBLIC eleos)
```
* cmkr.build
```toml
[fetch-content]
eleos = { git = "https://github.com/kusabana/eleos", tag = "1.0.0" }

[target.library]
link-libraries = ["eleos"]
```

### examples
```cpp
// sample interface
class sample_interface : public eleos::interface {
public:
  sample_interface( )
      : eleos::interface( "ISAMPLEINTERFACE001" ) {}
  ~sample_interface( ) = default;

  // ...
};

// examples of exposing an interface through
// multiple interface names (variadic)
class sample_variadic_interface : public eleos::interface {
public:
  sample_variadic_interface( )
      : eleos::interface(
            "ISAMPLEINTERFACE001",
            "ISAMPLEINTERFACE002",
            "ISAMPLEINTERFACE003" ) {}
  ~sample_variadic_interface( ) = default;

  // ...
};

// sample plugin
class sample_plugin
    : public eleos::interface
    , valve::plugin_callbacks::v4 {
public:
  sample_plugin( )
      : eleos::interface( "ISERVERPLUGINCALLBACKS004" ) {}
  ~sample_plugin( ) = default;

  // ...
  virtual auto load( void * /*unused*/, void * /*unused*/ ) -> bool {
    return false;
  }
  virtual auto unload( ) -> void {}
  virtual auto pause( ) -> void {}
  virtual auto unpause( ) -> void {}
  virtual auto description( ) -> const char * { return "sample_plugin"; }
}
```