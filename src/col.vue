<template>
   <div 
     class="col" 
     :class="colClasses"
     :style="colStyle"
     >
       <slot></slot>
   </div>
</template>

<script>
let validator = (value) =>{
    let keys = Object.keys(value);
    let val = true;
    keys.forEach(key=>{
        if (!['span','offset'].includes(key)) {
            val = false
        }
    })
    return val
}
export default {
    props:{
        span:{
            type:[Number,String],
        },
        offset: {
            type: [Number, String],
        },
        phone: {type: Object, validator,},
        ipad: {type: Object, validator,},
        narrowPc: {type: Object, validator,},
        pc: {type: Object, validator,},
        widePc: {type: Object, validator,}
    },
    data() {
        return {
            gutter: 0
        }
    },
    computed: {
        colClasses(){
            let {span,offset,phone,ipad,narrowPc,pc, widePc} = this
            let s = this.setClasses
            return [
                ...s({span,offset},''),
                ...s(phone,'phone-'),
                ...s(ipad,'ipad-'),
                ...s(narrowPc,'narrowPc-'),
                ...s(pc,'pc-'),
                ...s(widePc,'widePc-'),
                    ]
        },
        colStyle() {
            return {
                marginLeft: this.gutter/2 +'px',
                marginRight: this.gutter/2 +'px'
            }
        }
    },
    methods:{
        setClasses(obj,title='') {
            if (!obj) {
                return []
            }
            let arr = []
            if (obj.offset) arr.push(`offset-${title}${obj.offset}`);
            if (obj.span) arr.push(`col-${title}${obj.span}`);
            return arr
        }
    }

}
</script>

<style lang="scss" scoped>
.col {
    width: 50%;
    height: 100px;
    border: 1px solid red;
    background: #d3dce6;
    $class-prefix: col-;
    $class-offset: offset-;
    @for $n from 0 through 24 {
        &.#{$class-prefix}#{$n} {
            width: ($n/24)*100%;
        }
    }
    @for $n from 0 through 24 {
        &.#{$class-offset}#{$n} {
            margin-right: ($n/24)*100%;
        }
    }
    @media (max-width: 576px) {
        $class-prefix: col-phone-;
        @for $n from 1 through 24 {
        &.#{$class-prefix}#{$n} {
          width: ($n / 24) * 100%;
        }
      }
      $class-prefix: offset-phone-;
      @for $n from 1 through 24 {
        &.#{$class-prefix}#{$n} {
          margin-left: ($n / 24) * 100%;
        }
      }
    }
    @media (min-width: 577px) and (max-width: 768px) {
      $class-prefix: col-ipad-;
      @for $n from 1 through 24 {
        &.#{$class-prefix}#{$n} {
          width: ($n / 24) * 100%;
        }
      }
      $class-prefix: offset-ipad-;
      @for $n from 1 through 24 {
        &.#{$class-prefix}#{$n} {
          margin-left: ($n / 24) * 100%;
        }
      }
    }
    @media (min-width: 769px) and (max-width: 992px) {
      $class-prefix: col-narrow-pc-;
      @for $n from 1 through 24 {
        &.#{$class-prefix}#{$n} {
          width: ($n / 24) * 100%;
        }
      }
      $class-prefix: offset-narrow-pc-;
      @for $n from 1 through 24 {
        &.#{$class-prefix}#{$n} {
          margin-left: ($n / 24) * 100%;
        }
      }
    }
    @media (min-width: 993px) and (max-width: 1200px) {
      $class-prefix: col-pc-;
      @for $n from 1 through 24 {
        &.#{$class-prefix}#{$n} {
          width: ($n / 24) * 100%;
        }
      }
      $class-prefix: offset-pc-;
      @for $n from 1 through 24 {
        &.#{$class-prefix}#{$n} {
          margin-left: ($n / 24) * 100%;
        }
      }
    }
    @media (min-width: 1201px) {
      $class-prefix: col-wide-pc-;
      @for $n from 1 through 24 {
        &.#{$class-prefix}#{$n} {
          width: ($n / 24) * 100%;
        }
      }
      $class-prefix: offset-wide-pc-;
      @for $n from 1 through 24 {
        &.#{$class-prefix}#{$n} {
          margin-left: ($n / 24) * 100%;
        }
      }
    }
}
</style>
