# vue3 component 接口

- defineComponnets

  - 函数组件对比

    ```js
    vue2:{
      name: "HelloWorld",
      funtional:true,
      props: {
        msg: String,
      },
      mounted() {
        this.msg;
      },
    }
    vue3:export function
    ```

  - defineComponnets 源码

    ```ts
    efineComponent是一个实用程序，主要用于声明组件时的类型推断。类型推断在组件//选项中提供(作为参数提供)。返回值具有人工类型//用于TSX /手动渲染函数/ IDE支持。
    
    
    
    export type DefineComponent<
      PropsOrPropOptions = {},//props
      RawBindings = {},//setUp函数的返回值
      D = {},//data
      C extends ComputedOptions = ComputedOptions,//Computed
      M extends MethodOptions = MethodOptions,
      Mixin extends ComponentOptionsMixin = ComponentOptionsMixin,
      Extends extends ComponentOptionsMixin = ComponentOptionsMixin,
      E extends EmitsOptions = {},
      EE extends string = string,
      PP = PublicProps,
      Props = ResolveProps<PropsOrPropOptions, E>,
      Defaults = ExtractDefaultPropTypes<PropsOrPropOptions>,
      S extends SlotsType = {}
    > = ComponentPublicInstanceConstructor<
      CreateComponentPublicInstance<
        Props,
        RawBindings,
        D,
        C,
        M,
        Mixin,
        Extends,
        E,
        PP & Props,
        Defaults,
        true,
        {},
        S
      > &
        Props
    > &
      ComponentOptionsBase<
        Props,
        RawBindings,
        D,
        C,
        M,
        Mixin,
        Extends,
        E,
        EE,
        Defaults,
        {},
        string,
        S
      > &
      PP
    
    
    //重载1:直接设置函数
    //(使用用户定义的props接口)
    export function defineComponent<
      Props extends Record<string, any>,
      E extends EmitsOptions = {},
      EE extends string = string,
      S extends SlotsType = {}
    >(
      setup: (
        props: Props,
        ctx: SetupContext<E, S>
      ) => RenderFunction | Promise<RenderFunction>,
      options?: Pick<ComponentOptions, 'name' | 'inheritAttrs'> & {
        props?: (keyof Props)[]
        emits?: E | EE[]
        slots?: S
      }
    ): (props: Props & EmitsToProps<E>) => any
    export function defineComponent<
      Props extends Record<string, any>,
      E extends EmitsOptions = {},
      EE extends string = string,
      S extends SlotsType = {}
    >(
      setup: (
        props: Props,
        ctx: SetupContext<E, S>
      ) => RenderFunction | Promise<RenderFunction>,
      options?: Pick<ComponentOptions, 'name' | 'inheritAttrs'> & {
        props?: ComponentObjectPropsOptions<Props>
        emits?: E | EE[]
        slots?: S
      }
    ): (props: Props & EmitsToProps<E>) => any
    
    // overload 2: object format with no props
    // (uses user defined props interface)
    // return type is for Vetur and TSX support
    export function defineComponent<
      Props = {},
      RawBindings = {},
      D = {},
      C extends ComputedOptions = {},
      M extends MethodOptions = {},
      Mixin extends ComponentOptionsMixin = ComponentOptionsMixin,
      Extends extends ComponentOptionsMixin = ComponentOptionsMixin,
      E extends EmitsOptions = {},
      EE extends string = string,
      S extends SlotsType = {},
      I extends ComponentInjectOptions = {},
      II extends string = string
    >(
      options: ComponentOptionsWithoutProps<
        Props,
        RawBindings,
        D,
        C,
        M,
        Mixin,
        Extends,
        E,
        EE,
        I,
        II,
        S
      >
    ): DefineComponent<
      Props,
      RawBindings,
      D,
      C,
      M,
      Mixin,
      Extends,
      E,
      EE,
      PublicProps,
      ResolveProps<Props, E>,
      ExtractDefaultPropTypes<Props>,
      S
    >
    
    // overload 3: object format with array props declaration
    // props inferred as { [key in PropNames]?: any }
    // return type is for Vetur and TSX support
    export function defineComponent<
      PropNames extends string,
      RawBindings,
      D,
      C extends ComputedOptions = {},
      M extends MethodOptions = {},
      Mixin extends ComponentOptionsMixin = ComponentOptionsMixin,
      Extends extends ComponentOptionsMixin = ComponentOptionsMixin,
      E extends EmitsOptions = {},
      EE extends string = string,
      S extends SlotsType = {},
      I extends ComponentInjectOptions = {},
      II extends string = string,
      Props = Readonly<{ [key in PropNames]?: any }>
    >(
      options: ComponentOptionsWithArrayProps<
        PropNames,
        RawBindings,
        D,
        C,
        M,
        Mixin,
        Extends,
        E,
        EE,
        I,
        II,
        S
      >
    ): DefineComponent<
      Props,
      RawBindings,
      D,
      C,
      M,
      Mixin,
      Extends,
      E,
      EE,
      PublicProps,
      ResolveProps<Props, E>,
      ExtractDefaultPropTypes<Props>,
      S
    >
    
    // overload 4: object format with object props declaration
    // see `ExtractPropTypes` in ./componentProps.ts
    export function defineComponent<
      // the Readonly constraint allows TS to treat the type of { required: true }
      // as constant instead of boolean.
      PropsOptions extends Readonly<ComponentPropsOptions>,
      RawBindings,
      D,
      C extends ComputedOptions = {},
      M extends MethodOptions = {},
      Mixin extends ComponentOptionsMixin = ComponentOptionsMixin,
      Extends extends ComponentOptionsMixin = ComponentOptionsMixin,
      E extends EmitsOptions = {},
      EE extends string = string,
      S extends SlotsType = {},
      I extends ComponentInjectOptions = {},
      II extends string = string
    >(
      options: ComponentOptionsWithObjectProps<
        PropsOptions,
        RawBindings,
        D,
        C,
        M,
        Mixin,
        Extends,
        E,
        EE,
        I,
        II,
        S
      >
    ): DefineComponent<
      PropsOptions,
      RawBindings,
      D,
      C,
      M,
      Mixin,
      Extends,
      E,
      EE,
      PublicProps,
      ResolveProps<PropsOptions, E>,
      ExtractDefaultPropTypes<PropsOptions>,
      S
    >
    ```

    

